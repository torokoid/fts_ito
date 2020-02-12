# fts_ito

<html lang="ja">
 <head>
  <meta charset="utf-8" />
	 

<style type="text/css">

  p {
color: #fffafa;
font-size: 1.5em;
 }
<!--
 .red {color:#ff0000;}
 .grey {color:#999999;}
 .snow {color:#fffafa;}
 .yellow {color:#ff0000; background:#ffff00;}
 .blue {color:#0000ff;}
 .white {color:#ffffff; blinking;}
 .waku {border:2px dotted #99cc66;
　　　　　　line-height: 200%;
　　　　　　padding: 10px;}
 -->
	
.date:before{content:"20181115";}
	
	
 #preview{
	position: relative;
	border: 3px solid #333;
	background: #444;
	padding: 5px;
	display: none;
	color: #FFF;
	text-align: center;
}

main {
background-color: rgba(255, 255, 255, 0.3);
}

section {
background-color: rgba(0, 225, 0, 0.5);
}

#wrap {background:none} /*PC用の背景はオフ*/
body::before {
  content:"";
  display:block;
  position:fixed;
  top:0;
  left:0;
  z-index:-1;
  width:100%;
  height:100vh;
  background:url(https://torokoid.github.io/fts_furuhashi/20190417_002.jpg) center/cover no-repeat; /*fixedをトル！*/
  -webkit-background-size:cover;/*Android4*/
  }
 
@media	screen and (min-width: 540px),
	screen and (orientation: landscape) {
   p.note { display: none; }
}

/* 点滅 */
.blinking{
    -webkit-animation:blink 1.5s ease-in-out infinite alternate;
    -moz-animation:blink 1.5s ease-in-out infinite alternate;
    animation:blink 1.5s ease-in-out infinite alternate;
 } 
 @-webkit-keyframes blink{
     0% {opacity:0;}
     100% {opacity:1;}
 }
 @-moz-keyframes blink{
     0% {opacity:0;}
     100% {opacity:1;}
 }
 @keyframes blink{
     0% {opacity:0;}
     100% {opacity:1;}
}


/* 回転 */
.rotateX {
  background:rgba(255,0,0,0.8);
  width: 180px;
  height:35px;
  padding-top:0px;
  text-align: center;
	-webkit-animation: animeX 3s linear infinite;
	animation: animeX 3s linear infinite;
}

@-webkit-keyframes animeX {
	0%	{ -webkit-transform: rotateX(-0deg); }
	100%	{ -webkit-transform :rotateX(360deg); }
}
@keyframes animeX {
	0%	{ transform: rotateX(-0deg); }
	100%	{ transform :rotateX(360deg); }
}

.rotateY {
  background:rgba(255,0,0,0.8);
  width: 180px;
  height:35px;
  padding-top:0px;
  text-align: center;
	-webkit-animation: animeY 3s linear infinite;
	animation: animeY 3s linear infinite;
}

@-webkit-keyframes animeY {
	0%	{ -webkit-transform: rotateY(-0deg); }
	99.9%,to	{ -webkit-transform :rotateY(360deg); }
}
@keyframes animeY {
	0%	{ transform-origin: right bottom; }
	99.9%,to	{ transform:rotateY(360deg); }
}
  
  
  
  
a.p:hover {
    position: relative;
    text-decoration: none;
}
a.p span {
    display: none;
    position: relative;
    top: -0.5em;
    left: 1em;
}
a.p:hover span {
    border: none;
    display: block;
    width: 800px;
}   
    
 <!--
    p {
margin-left: 20px;
 }
    -->

.example {/*親div*/
  position: relative;/*相対配置*/
  }

.example p {
  position: absolute;/*絶対配置*/
  color: blue;/*文字は青に*/
  bottom: 0;
  right: 0;
  font-size: 1.0em;
  }
  
  
</style>

<link href="https://cdnjs.cloudflare.com/ajax/libs/lightbox2/2.7.1/css/lightbox.css" rel="stylesheet">
 
</head>
<body>
<p class="note">
  モバイル端末をお使いの場合は、画面を横向きにすると
  より見やすくご覧頂けます。
</p>
<p><a href="https://torokoid.github.io/fts_home">Home</a>>元FTS伊藤さん、矢口さん、小林実さんのご卒業記念バーティー</p>
<h2><span class="blue"><strong>簡易、支払い＆精算計算</strong></span></h2>


        
<section>

<ul>
<li> <input type="button" id="btn1" value="精算計算  " onclick="btn1Click();" /> 　←　支払い＆精算計算、開始ボタン</li>
</ul>
    
<script>  
//ボタン１をクリックした時の処理
function btn1Click(){ 

var selects = prompt('参加人数を入力！');

var selectss = prompt('支払った人の人数を入力！');

var koukin = prompt('繰り越し金額を入力！');
    
var nama = [];
    for (var i=0; i<selectss; i++){
      nama[i] = prompt("支払った人の名前を入力");
    }   

var menu = [];    
    for (var i=0; i<selectss; i++){
      menu[i] = prompt(nama[i] + "さんの支払金額を入力");
    } 

document.write("各自の支払金額は<br>")
    for (var i=0; i<menu.length; i++){
      document.write(nama[i] + "さん：" + menu[i] + "円 <br>")
    }
    
//各自の会計額を計算
    
var kasann = [];
      kasann[0] = menu[0];
    for (var i=0; i<selectss-1; i++){
kasann[i+1] = Math.round (Number(kasann[i]) + Number(menu[i+1]));
      }
    
var kasan = Math.round (Number(kasann[i]) - Number(koukin))
      
//各自の分担分を計算

var buntan = Math.round (Number(kasan)/Number(selects));

//各自の割り勘分を計算

var wari = [];
    for (var i=0; i<selects; i++){
    wari[i] = Math.round (Number(menu[i]) - Number(buntan));
      }

var kasann = kasann[selectss-1]
    
document.write("<br>経費の総額：" + kasann + "円<br>")
      
document.write("公金補助額：" + koukin + "円<br>")

document.write("精算金額の総額：" + kasan + "円<br>")

document.write("参加人数は：" + selects + "人<br>")
      
document.write("一人当たりの分担：" + buntan + "円<br>")

document.write("<br>支払った人への払い戻し金額は<br>")
    for (var i=0; i<menu.length; i++){
      document.write(nama[i] + "さん：" + wari[i] + "円 <br>")
    }

document.write ("<br>以上、お帰りも気を付けて、次回も元気に再会～(^^)/"); 

/*
document.write ("<br><br><h2><span class="yellow"><marquee behavior="alternate"><a href="https://torokoid.github.io/fts_furuhashi/">2018/11/15,古橋さんご卒業記念パーティー → 戻る !</a></marquee></span></h2> "); 
*/

document.write ("<br><br><br><br>Copyright 2019/12/03 S.Hada @ HGT 1G1");

        document.bgColor = "#00ff80";
        document.fgColor = "blue";
    
}

    </script>
    
        </section>

<h1><span class="yellow"><marquee behavior="alternate">!!! 背景画像は2019年4月17日(水)元FTS伊藤さんのご卒業記念お食事会 !!!</marquee></span></h1>	

<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
<!--
<p align="left"> <img src="QR_furuhashi.png" alt="アクセス用QRコード" width="100">アクセス用QRコード</p>
-->

<h1><span class="yellow"><marquee behavior="alternate">!!! 2020年1月24日(土)に元FTS伊藤さん、矢口さん、小林実さんのご卒業記念バーティー@魚盛 大宮店、が執り行われました !!!</marquee></span></h1>
<h2>
<SPAN style="margin-left:20px "><a href="https://r.gnavi.co.jp/g068264/map/" target="_blank" class="p">魚森map(クリックでリンク先に飛びます)<span><img src="https://torokoid.github.io/fts_furuhashi/uomori.JPG" alt="魚森map" width="1800"></span></a><br/> </SPAN></h2>

<!--
<SPAN style="margin-left:20px "><a href="https://r.gnavi.co.jp/g068264/map/" target="_blank" class="p"><img src="uomori.JPG" height="90" width="110" constrain="true" imagepreview="false">
     <span><img src="uomori.JPG" width="200" alt="Link拡大"></span></a></SPAN>
-->

<h2><span class="white">記念品目録</span></h2><br>
<h3><span class="white"><img src="https://torokoid.github.io/fts_furuhashi/ito.JPG" alt="サンプル画像" width="100" />for 伊藤さん</span></h3>
<a href="https://torokoid.github.io/fts_furuhashi/20200124_001.JPG" data-lightbox="abc"><img src="https://torokoid.github.io/fts_furuhashi/20200124_001.JPG" alt="サンプル画像" width="1800" /></a>
<h3><span class="white"><img src="https://torokoid.github.io/fts_furuhashi/yaguchi.JPG" alt="サンプル画像" width="100" />for 矢口さん</span></h3>
<a href="https://torokoid.github.io/fts_furuhashi/20200124_002.JPG" data-lightbox="abc"><img src="https://torokoid.github.io/fts_furuhashi/20200124_002.JPG" alt="サンプル画像" width="1800" /></a>
<h3><span class="white"><img src="https://torokoid.github.io/fts_furuhashi/kobayashi.JPG" alt="サンプル画像" width="100" />for 小林実さん</span></h3>
<a href="https://torokoid.github.io/fts_furuhashi/20200124_003.JPG" data-lightbox="abc"><img src="https://torokoid.github.io/fts_furuhashi/20200124_003.JPG" alt="サンプル画像" width="1800" /></a>
<h2><span class="white">矢口さん近況</span></h2>
<h3><span class="white">1218 ITS-J 卒業式</span></h3>
<a href="https://torokoid.github.io/fts_furuhashi/20200124_005.JPG" data-lightbox="abc"><img src="https://torokoid.github.io/fts_furuhashi/20200124_005.JPG" alt="サンプル画像" width="1800" /></a>
<h3><span class="white">FPC 卒業式</span></h3>
<a href="https://torokoid.github.io/fts_furuhashi/20200124_006.JPG" data-lightbox="abc"><img src="https://torokoid.github.io/fts_furuhashi/20200124_006.JPG" alt="サンプル画像" width="1800" /></a>
<h3><span class="white">ESMOスケールモデル</span></h3>
<a href="https://torokoid.github.io/fts_furuhashi/20200124_007.JPG" data-lightbox="abc"><img src="https://torokoid.github.io/fts_furuhashi/20200124_007.JPG" alt="サンプル画像" width="1800" /></a>
<h3><span class="white">ヤグチさん、すべて本</span></h3>
<a href="https://torokoid.github.io/fts_furuhashi/20200124_008.JPG" data-lightbox="abc"><img src="https://torokoid.github.io/fts_furuhashi/20200124_008.JPG" alt="サンプル画像" width="1800" /></a>
<h3><span class="white">ネスプレッソありがとう！</span></h3>
<a href="https://torokoid.github.io/fts_furuhashi/20200124_009.JPG" data-lightbox="abc"><img src="https://torokoid.github.io/fts_furuhashi/20200124_009.JPG" alt="サンプル画像" width="1800" /></a>

<h2><span class="white">実さん近況</span></h2>
<h3><span class="white">写真の自転車は、クロモリ、２０万円</span></h3>
<a href="https://torokoid.github.io/fts_furuhashi/20200124_004.JPG" data-lightbox="abc"><img src="https://torokoid.github.io/fts_furuhashi/20200124_004.JPG" alt="サンプル画像" width="1800" /></a>
<!--
<br><br><br>
<span class="red"><span class="blinking"><b><h1>実さん近況_2</h1></b></span></span><br>
-->
<h3><span class="white">水戸偕楽園 on 茂木・水戸・大洗、周遊コース</span></h3>
<a href="https://torokoid.github.io/fts_furuhashi/20200120_001.JPG" data-lightbox="abc"><img src="https://torokoid.github.io/fts_furuhashi/20200120_001.JPG" alt="サンプル画像" width="1800" /></a>
<h3><span class="white">自転車はピナレロ、フルカーボン、コンポはBSアルテグラ、トータル5０万円に進化、記念品フル装備！</span></h3>
<a href="https://torokoid.github.io/fts_furuhashi/20200120_002.JPG" data-lightbox="abc"><img src="https://torokoid.github.io/fts_furuhashi/20200120_002.JPG" alt="サンプル画像" width="1800" /></a>
<h3><span class="white">蕎麦の里まぎの on 茂木・水戸・大洗、周遊コース</span></h3>
<a href="https://torokoid.github.io/fts_furuhashi/20200120_003.JPG" data-lightbox="abc"><img src="https://torokoid.github.io/fts_furuhashi/20200120_003.JPG" alt="サンプル画像" width="1800" /></a>

<!--
<a href="https://torokoid.github.io/fts_furuhashi/20190417_002.jpg" data-lightbox="abc"><img src="https://torokoid.github.io/fts_furuhashi/20190417_002.jpg" alt="サンプル画像" width="1800" /></a>
<br><br><br><br><br>
-->

<p align="right"><marquee direction="right" scrollamount="20" width="30%">(^_^)/~hada</marquee></p>
<br><br><br><br><br><br><br><br><br><br>
<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
<h3><span class="white">「魚盛」にて</span></h3>
<a href="20200124_001.JPG" data-lightbox="abc"><img src="20200124_001.JPG" alt="サンプル画像" width="200" /></a>
<a href="20200124_002.JPG" data-lightbox="abc"><img src="20200124_002.JPG" alt="サンプル画像" width="200" /></a>
<a href="20200124_003.JPG" data-lightbox="abc"><img src="20200124_003.JPG" alt="サンプル画像" width="200" /></a>
<a href="20200124_004.JPG" data-lightbox="abc"><img src="20200124_004.JPG" alt="サンプル画像" width="200" /></a>
<a href="20200124_005.JPG" data-lightbox="abc"><img src="20200124_005.JPG" alt="サンプル画像" width="200" /></a>
<a href="20200124_006.JPG" data-lightbox="abc"><img src="20200124_006.JPG" alt="サンプル画像" width="200" /></a>
<a href="20200124_007.JPG" data-lightbox="abc"><img src="20200124_007.JPG" alt="サンプル画像" width="200" /></a>
<a href="20200124_008.JPG" data-lightbox="abc"><img src="20200124_008.JPG" alt="サンプル画像" width="200" /></a>
<a href="20200124_009.JPG" data-lightbox="abc"><img src="20200124_009.JPG" alt="サンプル画像" width="200" /></a>
<a href="20200124_010.JPG" data-lightbox="abc"><img src="20200124_010.JPG" alt="サンプル画像" width="200" /></a>
<a href="20200124_011.JPG" data-lightbox="abc"><img src="20200124_011.JPG" alt="サンプル画像" width="200" /></a>
<a href="20200124_012.JPG" data-lightbox="abc"><img src="20200124_012.JPG" alt="サンプル画像" width="200" /></a>
<h3><span class="white">お孫さんシリーズ</span></h3>
<a href="20200124_025.JPG" data-lightbox="abc"><img src="20200124_025.JPG" alt="サンプル画像" width="200" /></a>
<h3><span class="white">お孫さんシリーズ、横山さん</span></h3>
<a href="20200124_026.JPG" data-lightbox="abc"><img src="20200124_026.JPG" alt="サンプル画像" width="200" /></a>
<iframe width="560" height="315" src="https://www.youtube.com/embed/p2-fgK6S61U" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<h3><span class="white">矢口さんからのプレゼント</span></h3>
<a href="20200124_013.JPG" data-lightbox="abc"><img src="20200124_013.JPG" alt="サンプル画像" width="200" /></a>
<a href="20200124_027.JPG" data-lightbox="abc"><img src="20200124_027.JPG" alt="サンプル画像" width="200" /></a>
<h3><span class="white">ヤグチさん、すべて本、1枚目と2枚目は差し替え画像・・・間違え探し</span></h3>
<a href="20200124_014.JPG" data-lightbox="abc"><img src="20200124_014.JPG" alt="サンプル画像" width="400" /></a>
<a href="20200124_028.JPG" data-lightbox="abc"><img src="20200124_028.JPG" alt="サンプル画像" width="400" /></a>
<a href="20200124_015.JPG" data-lightbox="abc"><img src="20200124_015.JPG" alt="サンプル画像" width="200" /></a>
<a href="20200124_016.JPG" data-lightbox="abc"><img src="20200124_016.JPG" alt="サンプル画像" width="200" /></a>
<a href="20200124_017.JPG" data-lightbox="abc"><img src="20200124_017.JPG" alt="サンプル画像" width="400" /></a>
<a href="20200124_018.JPG" data-lightbox="abc"><img src="20200124_018.JPG" alt="サンプル画像" width="400" /></a>
<a href="20200124_019.JPG" data-lightbox="abc"><img src="20200124_019.JPG" alt="サンプル画像" width="400" /></a>
<a href="20200124_020.JPG" data-lightbox="abc"><img src="20200124_020.JPG" alt="サンプル画像" width="400" /></a>
<a href="20200124_021.JPG" data-lightbox="abc"><img src="20200124_021.JPG" alt="サンプル画像" width="400" /></a>
<a href="20200124_022.JPG" data-lightbox="abc"><img src="20200124_022.JPG" alt="サンプル画像" width="400" /></a>
<a href="20200124_023.JPG" data-lightbox="abc"><img src="20200124_023.JPG" alt="サンプル画像" width="400" /></a>
<a href="20200124_024.JPG" data-lightbox="abc"><img src="20200124_024.JPG" alt="サンプル画像" width="400" /></a>
<h3><span class="white">伊藤さんご挨拶</span></h3>
<iframe width="560" height="315" src="https://www.youtube.com/embed/vNdcVrdJJ-I" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<h3><span class="white">矢口さんご挨拶</span></h3>
<iframe width="560" height="315" src="https://www.youtube.com/embed/LzUUGUukOqY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<iframe width="560" height="315" src="https://www.youtube.com/embed/_yDNCzxO5uc" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<h3><span class="white">小林実さんご挨拶</span></h3>
<iframe width="560" height="315" src="https://www.youtube.com/embed/vgKQ6kX8ip0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<h3><span class="white">横山さんご挨拶</span></h3>
<iframe width="560" height="315" src="https://www.youtube.com/embed/3UOAAOK0Z74" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>	
	
	

<script src="https://code.jquery.com/jquery-1.12.4.min.js" type="text/javascript"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/lightbox2/2.7.1/js/lightbox.min.js" type="text/javascript"></script>


<br><br><br><br><br><br><br><br><br><br><br><br><br><br>

<script type='text/javascript' src='https://torokoid.github.io/shiba/jquery.js?ver=1.12.4'></script>
<script src="https://torokoid.github.io/shiba/jquery.goup.min.js"></script>
<script src="https://torokoid.github.io/shiba/my.js"></script> 

</body>

<!-- フッタ -->
 <footer><span class="snow">
 Copyright 2020/01/24 S.Hada
	</span></footer>
