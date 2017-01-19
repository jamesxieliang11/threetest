index.html: 
    可控制立方体组 
    控件js/TrackballControls.js （待自改）
    canvas引入webgl API（构造立方体）
    requestanimateframe实现动态渲染（动画和控制实时刷新）

geometry_earth.html：

    控件代码

    function onDocumentMouseMove( event ) {
	mouseX = ( event.clientX - windowHalfX );
	mouseY = ( event.clientY - windowHalfY );
    }

其中windowHalfX和windowHalfY都是当前窗口的一半高和宽
windowHalfX = window.innerWidth / 2;
windowHalfY = window.innerHeight / 2;
上文有定义

clientX 设置或获取鼠标指针位置相对于窗口客户区域的 x 坐标
clientY 设置或获取鼠标指针位置相对于窗口客户区域的 y 坐标

那么mouseX，mouseY即当前鼠标位置距窗口中心位置的差值

之所以选择中心位置是因为球体一直在中心位置，（windowHalfX，windowHalfY）为球心位置，（clientX，clientY）为鼠标指针位置

    camera.position.x += ( mouseX - camera.position.x ) * 0.05;
    camera.position.y += ( - mouseY - camera.position.y ) * 0.05;
相机左右移动的函数


    camera.lookAt( scene.position );
点睛代码（相机对准物体）此代码为three.js核心代码之一

下面开始详细解析该代码（其实也就简单的一句话）
    camera.lookAt(scene.position),会是相机对准场景（因为我们的球体在场景中），而相机的position（x，y）是在变化的position.z是固定的（可查看代码）
    大可注释掉group.rotation.y -= 0.005这段让球体自动旋转的代码即可查看到效果 发现远近交互的效果

testmesh.html

    粗糙的纹理应用，即纹理贴在立方体上
    主要代码
    var cubeMaterialss=new THREE.MeshBasicMaterial({map:new THREE.ImageUtils.loadTexture('images/3.jpg')});
    对loadTexture的应用

threetest2.html
    主要代码
    var textureCube = THREE.ImageUtils.loadTextureCube(urls, new THREE.CubeReflectionMapping());
    对loadTextureCube的应用

td_eyes.html
    全景图（贴在立方体上）
    对六张图图片要求很高 是一张全景图处理成的六张图片 可使用blender插件处理 也可上网上下载全景图片
