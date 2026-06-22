# parallel residual network with VAE reconstruct error

這裡VAE只針對少數類別進行one class訓練，訓練完後的VAE可以用來sampling new training data，以及將所有的training data從新餵進去VAE裡，讓VAE從新decode。因為VAE只有經過少數類別的訓練，所以當少數類別重構時，再用原資料減去重構資料的兩者誤差會非常的小，但若是沒見過的不平衡多數類別，因為VAE沒見過，所以重構誤差會非常的大，這有利於下面的parallel residual network進行辨別。

而下面的parallel residual network，則有著多條平行網路(預設五條)，每條內有residual block(預設五個)，經過平行網路後進行short cut，最後經過element gate，篩選重要的特徵並給予較高的權重。

此網路設計於應對不平衡醫學資料集
