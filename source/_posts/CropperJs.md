# cropperJs

### 1.cropperjs 是什么

一款 Javascript 图像裁剪器 

github文档：https://github.com/fengyuanchen/cropperjs/blob/main/README.md

### 2.具体用法

##### a.准备工作

第一步，引入cropperjs包

```
npm install cropperjs
or
yarn add cropperjs
```

第二步，首先我们需要有一个container容器来保存一个 img 或 canvas， 此处我们以img为例。

```
<div className='container'>
     <img id='image' ref={imgref} src={imgURL}/>	
</div>
```

第三步，我们要设置img的样式，这很重要！

```
#image {
    display: block;
    max-width: 100%;
}
```

第四步，我们要引入 cropper.css这个文件，如果不引入这个文件，就无法达到裁剪器的效果。该css文件在node-modules/cropperjs/dist目录下。

##### b.开始使用

```
export default function Crop () {
    const [imgURL,setimgURL] = useState(pic)
    const imgref = useRef()
    useEffect(()=>{
        // 创建一个Cropper实例
        // 第一个参数，html元素，img或canvas
        // 第二个参数，一个对象，在该对象内可以自定义裁剪组件属性的值，详情见文档
       	// 这里列出常用到的属性
        const cropper = new Cropper(imgref.current,{
             aspectRatio:1/1, // 指裁剪框的横纵比
             viewMode:1, // 主要用于设置裁剪框的作用区域
             dragMode:2, // 裁剪框拖动模式
             cropBoxMovable:true, // 裁剪框能否移动
             cropBoxResizable:false, // 裁剪框能否重新调整大小
             zoomOnWheel:true, // 能否通过鼠标滚轮来缩放图片大小
             zoomOnTouch:true, // 能否通过触摸来缩放图片大小
             preview:document.querySelectorAll('#preview'), //用于预览将要裁剪的图片
        })
    },[])
    return (
        <div className='box'>
            <div className='container'>
                <img id='image' ref={imgref} src={imgURL}/>
            </div>
            <div id='preview'></div>
        </div>
    )
}

```

当cropper对象生成时，裁剪器就会被渲染出来了，以上Crop便是一个裁剪组件
