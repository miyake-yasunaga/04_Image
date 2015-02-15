-----------------------------------
#Androidアプリのプログラムに挑戦  
画像の処理　その２（画像の切り替え）  
-----------------------------------

ボタンを押すと画像が切り替わるようにしてみましょう。  

![10](https://github.com/miyake-yasunaga/04_Image/blob/master/images/10.png)

02_Buttonの文字列の切り替えと同じように  
ボタンを押下したときに、画像を切り替えてみます。  

画像を背景として設定するsetBackgroundResourceという  
メソッドがあるのでこれを使ってみましょう。  

事前準備として、変更したい画像ファイルを「image02」という名前で  
app\src\res\drawableの下に追加しておいてください。  

![00](https://github.com/miyake-yasunaga/04_Image/blob/master/images/00.png)


１．XMLにImageViewのウィジェットを追加しているので  
ImageViewを扱うパッケージを追加します。  

        import android.widget.ImageView;  

２．TextViewの時と同じようにImageView型の変数を「im01」を宣言して  
表示したい場所のIDを設定します。  

        final ImageView im01 = (ImageView)this.findViewById(R.id.imageView);  

３．上で指定した「im01」の背景に指定した画像を設定します。  

        im01.setBackgroundResource(R.drawable.image02);  

![01](https://github.com/miyake-yasunaga/04_Image/blob/master/images/01.png)


特にエラーもでませんでした。  
結構簡単でしたね。  

では早速、ビルドしてみましょう。  

![02](https://github.com/miyake-yasunaga/04_Image/blob/master/images/02.png)

・・・ボタンを押すと背景に画像が出てきてるようですが  
最初の画像が表示されたままでうまく切り替えできませんでした。  

なにかいい方法はないでしょうか・・・  

画像表示のメソッドが他にないか、ちょっと調べてみると  
setImageBitmapというメソッドを見つけました。  

使い方はよくわかってませんが、とりあえずやってみましょう。  

setBackgroundResourceメソッドをコメントアウトして  
同じようにsetImageBitmapメソッドを記述してみます。  

          //im01.setBackgroundResource(R.drawable.image02);  
          im01.setImageBitmap(R.drawable.image02);  

なにか吹き出しがでてきました。  
「setImageBitmapにはint型は渡せません。Bitmap型を渡しなさい。」  
と言ってます。  
（R.drawable.image02というのはプログラムの中でidに変換されてint型になってるようです）  

![03](https://github.com/miyake-yasunaga/04_Image/blob/master/images/03.png)

とりあえず、Bitmap型の変数bmを宣言します。  
あ、また吹き出しが出て来ました。  

![04](https://github.com/miyake-yasunaga/04_Image/blob/master/images/04.png)

android.graphics.Bitmapのパッケージがimportされてないと  
言ってるようです。言われたとおりAlt+Enterを押すと  

          import android.graphics.Bitmap;  

が追加されました。  

続いて画像をBitmap型にセットします。  
Webなどで調べると、BitmapFactoryのdecodeResourceメソッドを  
使えばいいとのことなのでとりあえず書いてみます。  

           bm = BitmapFactory.decodeResource();  

また、吹き出しが出ました。  

今度はandroid.graphics.BitmapFactoryのパッケージがimportされてないと  
言ってるようです。  

１行書くたびに怒られてしまいますね・・・  

言われたとおりAlt+Enterを押して追加します。  

![06](https://github.com/miyake-yasunaga/04_Image/blob/master/images/06.png)


          import android.graphics.BitmapFactory;  
が追加されました。  

またまた吹き出しが・・・  

「BitmapFactory.decodeResource();  
の（）の中にはリソースと画像のIdをセットしろ」と言ってます。  

![07](https://github.com/miyake-yasunaga/04_Image/blob/master/images/07.png)

リソースって何をセットすればいいのかよくわからないので  
またWebで調べてみます。  

           Resources res = getResources();  

って書けばいいようです。  
これで自分の持ってるリソース（宣言してるテキストや画像）を扱えるようになるみたいです。  

実際に書いてみると、また吹き出しで  
android.content.res.Resourcesのパッケージがimportされてないとの事・・・  
これもAlt+Enterを押して追加します。  

![08](https://github.com/miyake-yasunaga/04_Image/blob/master/images/08.png)


BitmapFactory.decodeResourceに上で宣言した  
Resources型の「res」とint型の画像のid「R.drawable.image02」を設定します。  

最後にsetImageBitmapメソッドにBitmap型の「bm」を設定します。  

                bm = BitmapFactory.decodeResource(res,R.drawable.image02);  
                im01.setImageBitmap(bm);  

やっと、吹き出しがでなくなりました！！  

![09](https://github.com/miyake-yasunaga/04_Image/blob/master/images/09.png)

では、ビルドしてみましょう。  

ボタンを押すと・・・きれいに画像が切り替わりました！！  

![10](https://github.com/miyake-yasunaga/04_Image/blob/master/images/10.png)

数行のコードを書くだけでしたが  
結構大変でした。  

サンプルをコピペとかすれば、楽ですが  
自分で１行１行書いていくと  
やはり理解が深まっていくような気がしますね。  

間違えたり、足りない部分は吹き出しが助けてくれるので  
分からなくても、取りあえず書いて調べて  
トライアンドエラーで頑張っていきましょう！  

