---
layout: post
category: "read"
title:  bilibili 直播挂机
tags: [bilibili,直播挂机]
---


    onlineHeart.php
    bilibili 直播挂机，通过不断向服务器发送心跳包，达到欺骗目的从而实现 24H 涨经验升级
    
    说明：上传 PHP 文件后，在头部修改为自己的 B 站 Cookie，进行一次手动测试，访
    
    问该页面看到
    
    [2016-10-04 22:34:06]
     > INFO: already send @ 2016-10-04 22:30:01
    ===============================
    name: 雪狼meto
    level: 21
    exp: 4573000/8000000 57.16%
    sign: 今天已签到过
    ===============================
    的字样即为成功，然后设置服务器 5 分钟访问一次该页面即可实现挂机（crontab 或者第三方监控服务）


        <?php
    /**
     *  Author： METO
     *  Version: 0.2.0
     */
    class bilibili{
    	public $user=array(
    		array(
    			'cookie' => '填写用户cookie',
    			'status' => 1,
    		),
    		array(
    			'cookie' => '第二个用户cookie',
    			'status' => 0, // 0 表示禁用
    		),
            // 多用户以此类推
    	);
    	public function display(){
    		header('Content-Type: text/txt; charset=UTF-8');
    		echo "===============================\n";
    		foreach($this->user as $result){
    			if($result['status']){
    				$data=$result['data'];
    				$a=$data['data']['user_intimacy'];
    		        $b=$data['data']['user_next_intimacy'];
    		        $per=round($a/$b*100,2);
    				if(!isset($result['cron']['data'][1]))$msg='OK';
    				else $msg='@'.date('Y-m-d H:i:s',$result['cron']['data'][1]);
    		        echo "name   : {$data['data']['uname']} \n";
    		        echo "level  : {$data['data']['user_level']} \n";
    		        echo "exp    : {$a}/{$b} [{$per}%]\n";
    				echo "status : {$msg}\n";
    		        echo "===============================\n";
    			}
    			else{
    				echo "status : {$result['data']['msg']}\n";
    		        echo "===============================\n";
    			}
    		}
    	}
        public function cron(){
    		$mh=curl_multi_init();
    		foreach($this->user as $id=>$user){
    			if($user['status']!=1)continue;
    			$curl[$id]=$this->create('http://live.bilibili.com/User/userOnlineHeart',$user['cookie']);
    			curl_multi_add_handle($mh,$curl[$id]);
    		}
    		do{
    		    curl_multi_exec($mh,$running);
    		    curl_multi_select($mh);
    		}while($running>0);
    		foreach($curl as $id=>$c){
    			$result[$id]=curl_multi_getcontent($c);
    			curl_multi_remove_handle($mh,$c);
    		}
    		curl_multi_close($mh);
    		foreach($result as $id=>$vo){
    			$vo=json_decode($vo,1);
    			$this->user[$id]['cron']=$vo;
    		}
        }
    	public function check(){
    		$mh=curl_multi_init();
    		foreach($this->user as $id=>$user){
    			if($user['status']!=1)continue;
    			$curl[$id]=$this->create('http://live.bilibili.com/User/getUserInfo',$user['cookie']);
    			curl_multi_add_handle($mh,$curl[$id]);
    		}
    		do{
    		    curl_multi_exec($mh,$running);
    		    curl_multi_select($mh);
    		}while($running>0);
    		foreach($curl as $id=>$c){
    			$result[$id]=curl_multi_getcontent($c);
    			curl_multi_remove_handle($mh,$c);
    		}
    		curl_multi_close($mh);
    		foreach($result as $id=>$vo){
    			$vo=json_decode($vo,1);
    			if($vo['code']<0)$this->user[$id]['status']=0;
    			$this->user[$id]['data']=$vo;
    		}
    	}
    	private function create($url,$cookie){
    		$curl=curl_init();
            curl_setopt($curl,CURLOPT_URL,$url);
    		curl_setopt($curl,CURLOPT_COOKIE,$cookie);
            curl_setopt($curl,CURLOPT_RETURNTRANSFER, 1);
            curl_setopt($curl,CURLOPT_CONNECTTIMEOUT, 10);
            curl_setopt($curl,CURLOPT_REFERER,'http://live.bilibili.com/');
            curl_setopt($curl,CURLOPT_USERAGENT,'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_6_8) AppleWebKit/536.5 (KHTML, like Gecko) Chrome/19.0.1084.56 Safari/536.5');
    		return $curl;
    	}
    }
    $API=new bilibili;
    $API->check();
    $API->cron();
    $API->display();