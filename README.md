# 在web端展示最新的微信表情-截止日期为2021-05-21


![图片](https://user-images.githubusercontent.com/7782436/119081869-79863580-ba2f-11eb-8c96-79582197d7cf.png)

1. 准备雪碧图
    雪碧图: /public/static/faces.png  雪碧图尺寸1320 × 538，表情大小68 x 68 间距10,4倍缩放时(68+10)/4=19.5
2. 准备包含表情含义的测试文本
    ```
        let str = '[微笑], [撇嘴], [色], [发呆], [得意]';
    ```
3. 核心转换函数
    ```
    let arr = [
        '[微笑]', '[撇嘴]', '[色]', '[发呆]', '[得意]',
        '[流泪]', '[害羞]', '[闭嘴]', '[睡]', '[大哭]',
        '[尴尬]', '[发怒]', '[调皮]', '[呲牙]', '[惊讶]',
        '[难过]', '[囧]', '[抓狂]', '[吐]', '[偷笑]',
        '[愉快]', '[白眼]', '[傲慢]', '[困]', '[惊恐]',
        '[憨笑]', '[悠闲]', '[咒骂]', '[疑问]', '[嘘]',
        '[晕]', '[衰]', '[骷髅]', '[敲打]', '[再见]',
        '[擦汗]', '[抠鼻]', '[鼓掌]', '[坏笑]', '[右哼哼]',
        '[鄙视]', '[委屈]', '[快哭了]', '[阴险]', '[亲亲]',
        '[可怜]', '[笑脸]', '[生病]', '[脸红]', '[破涕为笑]',
        '[恐惧]', '[失望]', '[无语]', '[嘿哈]', '[捂脸]',
        '[奸笑]', '[机智]', '[皱眉]', '[耶]', '[吃瓜]',
        '[加油]', '[汗]', '[天啊]', '[Emm]', '[社会社会]',
        '[旺柴]', '[好的]', '[打脸]', '[哇]', '[翻白眼]',
        '[666]', '[让我看看]', '[叹气]', '[苦涩]', '[裂开]',
        '[嘴唇]', '[爱心]', '[心碎]', '[拥抱]', '[强]',
        '[弱]', '[握手]', '[胜利]', '[抱拳]', '[勾引]',
        '[拳头]', '[OK]', '[合十]', '[啤酒]', '[咖啡]',
        '[蛋糕]', '[玫瑰]', '[凋谢]', '[菜刀]', '[炸弹]',
        '[便便]', '[月亮]', '[太阳]', '[庆祝]', '[礼物]',
        '[红包]', '[發]', '[福]', '[烟花]', '[爆竹]',
        '[猪头]', '[跳跳]', '[发抖]', '[转圈]', '[流汗]',
        '[西瓜]', '[左哼哼]', '[怄火]', '[哈欠]', '[奋斗]', '[鬼魂]', '[小狗]'
    ];
   function  textConvert (content) {
    let text = content;
    let regex2 = /\[(.+?)\]/g; // [] 中括号
    // 输出是一个数组
    let strArrow = text.match(regex2);
    if (strArrow?.length > 0) {
      strArrow. forEach((element)=> {
        let idx = arr.indexOf(element); 
        // 计算坐标
        let xPoint = (idx % 17) * 19.5;
        let yPoint = Math.floor(idx / 17) * 19.5;
        let style = `display:inline-block;background-position:${-xPoint}px ${-yPoint}px;width:18px;height:18px;background-repeat:no-repeat;background-image:url(../public/static/faces.png);background-size:330px 134.5px`;
        text = text.replace(element, `<div style='${style}'></div>`);
      });
    }
    return text;
   }
   ```
  
4. 调用文本转换表情图片的方法,将转换结果在页面输出
    ```
      let textResult = textConvert(str);
      document.querySelector('#result').innerHTML = textResult;
    ```
    
5. 示例文件 src/index.html
