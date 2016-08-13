# snake
only use javascript to achieve the snake
coding...

<html>
<head>
	<style type="text/css">
	.bor{border:1px solid black;margin:0 auto}
	.ele{border:1px solid white;position:relative;background-color:white}
	</style>
</head>
<body>
	<div id="countdiv" align="center" style="font-size:30px;font-weight:bolder">option:W,S,A,D</br></br>score:0</div>
	<script type="text/javascript">
		var size=20,rownum=12,colnum=12,randomId,count=0,dire="up",undire="down",array=new Array(),randArray=new Array();//rownum,colnum:number of elediv
		var bordiv=document.createElement("div");
		bordiv.className="bor";
		bordiv.style.width=rownum*size+2;
		bordiv.style.height=colnum*size+2;
		for(var i=0;i<colnum;i++){
			for(var j=0;j<rownum;j++){
				var elediv=document.createElement("div");
				elediv.className="ele";
				elediv.style.width=size;
				elediv.style.height=size;
				elediv.style.left=size*j;
				elediv.style.top=size*i+size+2;
				elediv.style.marginTop=-(size+2);
				bordiv.appendChild(elediv);
				elediv.setAttribute("id",(size*j).toString()+(size*i+size+2));
				!(parseInt(rownum/2)==j&&parseInt(colnum/2)==i)?randArray.push((size*j).toString()+(size*i+size+2)):array.push((j*size).toString()+(i*size+size+2));
			}
		}
		document.body.appendChild(bordiv);
		randomId=randArray.splice(parseInt(Math.random()*randArray.length),1);
		document.getElementById(randomId).style.backgroundColor="blue";
		var headPush=function(id){
			array.unshift(id);
			randArray.indexOf(id)!=-1?randArray.splice(randArray.indexOf(id),1):null;
			document.getElementById(id).style.backgroundColor="black";
		}
		var gameOver=function(end){
			alert(end+"\nscore:"+count);
			clearInterval(interval);
		}
		var interval=window.setInterval(function(){
			var first=document.getElementById(array[0]);
			var x=parseInt(first.style.left);
			var y=parseInt(first.style.top);
			var tempx=x,tempy=y;
			dire=="left"?(x==0?x=size*(rownum-1):x-=size):dire=="right"?(x==size*(rownum-1)?x=0:x+=size):dire=="up"?(y==size+2?y=size*(colnum-1)+size+2:y-=size):dire=="down"?(y==size*(colnum-1)+size+2?y=size+2:y+=size):alert("error");
			var id=x.toString()+y;
			if(randomId!=id){
				var tailId=array.pop();
				randArray.push(tailId);
				document.getElementById(tailId).style.backgroundColor="white";
			}else{
				randArray.length!=0?randomId=randArray.splice(parseInt(Math.random()*randArray.length),1):gameOver("YOU WIN");
				document.getElementById(randomId).style.backgroundColor="blue";
				document.getElementById("countdiv").innerHTML="option:W,S,A,D</br></br>score:"+(++count);
			}
			array.indexOf(id)==-1?headPush(id):gameOver("Game Over");
			array.length==1?undire=null:x-tempx>0?(x-tempx==size?undire="left":undire="right"):x-tempx<0?(x-tempx==-size?undire="right":undire="left"):y-tempy>0?(y-tempy==size?undire="up":undire="down"):y-tempy<0?(y-tempy==-size?undire="down":undire="up"):alert("error");
		},100);//speed
		document.onkeydown=function(event){
			var e = event || window.event || arguments.callee.caller.arguments[0];
			var key=String.fromCharCode(e.keyCode);
			key=="W"?(undire=="up"?null:dire="up"):key=="S"?(undire=="down"?null:dire="down"):key=="A"?(undire=="left"?null:dire="left"):key=="D"?(undire=="right"?null:dire="right"):null;
		}
	</script>
</body>
</html> 
