#
```
https://medium.com/deep-learning-turkey/google-colab-free-gpu-tutorial-e113627b9f5d
https://blog.csdn.net/lomodays207/article/details/87267794
```

#
```
!wget https://raw.githubusercontent.com/keras-team/keras/master/examples/mnist_cnn.py

!python mnist_cnn.py
```
#
```
!wget https://raw.githubusercontent.com/vincentarelbundock/Rdatasets/master/csv/datasets/Titanic.csv -P "/content/drive/My Drive/app"

import pandas as pd
titanic = pd.read_csv('/content/drive/My Drive/app/Titanic.csv')
titanic.head(5)
```
#
```
from google.colab import files
uploaded = files.upload()


 !python3 "/content/drive/My Drive/app/mnist_cnn.py"
 
 https://github.com/keras-team/keras/blob/master/examples/mnist_cnn.py
```

#
```
!pip install -q xgboost==0.4a30
import xgboost
```
