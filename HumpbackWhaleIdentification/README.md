# HumpbackWhaleIdentification
The competition home is 
<a href=https://www.kaggle.com/c/humpback-whale-identification>
https://www.kaggle.com/c/humpback-whale-identification
</a>
  
This is my note of what I do(or did) in this competiton. At first written in Japanese. And then written in English.  

## コンペ概要
クジラのしっぽ画像からクジラの種類を分類する画像分類コンペだった。特徴としては2万5千枚くらいの画像に対し、未分類的な扱いの
new_whaleが9000枚以上存在し、それ以外の最も画像が多い種類は96枚。2500種以上は画像がたった1枚しかないOne-Shot-Learningが必要なコンペ。

## コンペの結果
66/2131 で上位4％に入ることができた。初メダルの思い出深きコンペ。

## このコンペで重要だった技術
### Siamese Network
One-Shot-Learning の代表例。2つのCNNを並列に並べて同じ画像であれば距離を近く、別の画像は遠くなるように学習する。
具体的には高次元空間にどうやって配置するか(どのように画像をベクトル化するか)を学習する。
lossはTriplet lossを使用した。これはアンカー画像を1枚用意し、アンカーと同じクラスなら近く、違うクラスなら遠くに配置するように学習するもの。
  
Courseraのdeeplearning.aiでとても分かりやすく説明されている。
### Image Hash
同じ画像が複数紛れ込んでいたのでハッシュ化して同じものがあったら除外する方法が公開された。素晴らしい発想。Siamese Networkについても解説がある。
<a href=https://www.kaggle.com/martinpiotte/whale-recognition-model-with-score-0-78563>
https://www.kaggle.com/martinpiotte/whale-recognition-model-with-score-0-78563
</a>
  
  
上記を発展させた<a href=https://www.kaggle.com/seesee/siamese-pretrained-0-822>
このkernel
</a>
をメインにして、lap を lapjvに変更し、Colabで実行するように変更(毎回重みをクラウドストレージに退避する処理を追加)
したモデルが一番良かった。

## その他試したこと
### ArcFaceLoss
顔認証で使われるloss画像の類似度を距離でなくcos類似度で測る。うまくいくと思ったのだが前処理で間違えていたため精度が出なかった。
loss自体は
<a href=https://gist.github.com/koshian2/d28a3cbdfc8f398f7d836739dbc6b5b2>
こちら
</a>
を参考にした。(精度が出なかったのは前処理の問題なので、こちらの問題ではないです)

### AffinityLoss
<a href=https://arxiv.org/abs/1901.07711>
https://arxiv.org/abs/1901.07711
</a>
  
不均衡データの分類に対するloss関数。コンペ終了約1ヶ月前に出た論文で、モデルへの適用が間に合わなかった。。。実装された方がいるので
<a href=https://github.com/koshian2/affinity-loss>
こちら
</a>
を参考にする予定
