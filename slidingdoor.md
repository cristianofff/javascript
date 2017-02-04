# javascript
Sliding door effect
window.onload = function(){

	//容器对象
	var box = document.getElementById("continer");

	//获得图片的NodeList对象集合
	var imgs = box.getElementsByTagName("img");

	//单张图片宽度
	var imgwidth = imgs[0].offsetWidth;

	//设置掩藏门体的宽度
	var exposewidth = 260;

	//设置容器的总宽度
	var boxwidth = imgwidth + (imgs.length - 1) * exposewidth;
	box.style.width = boxwidth + 'px';

	//设置每道门的初始位置
	function setImgPos(){
		for (var i = 1,len = imgs.length; i<len ; i++) {
			imgs[i].style.left = imgwidth + exposewidth * (i - 1) + 'px';
		}
	}setImgPos();

	//计算每道门打开时应移动的距离
	var translate = imgwidth - exposewidth;

	//为每道门绑定事件
	for (var i = 0,len = imgs.length; i<len ; i++) {

		//使用立即调用的函数表达式，为了获得不同的i值
		(function(i){
			imgs[i].onmouseover = function(){
				//先将每道门复位
				setImgPos();
				//打开门
				for (var j = 1; j <= i; j++) {
					imgs[j].style.left = parseInt(imgs[j].style.left,10) - translate + 'px'
				}
			};
		})(i);
	}
}
