## Propagation



- ### 순전파

  ![image-20210402180055724](C:\Users\winner\AppData\Roaming\Typora\typora-user-images\image-20210402180055724.png)

  ##### 여기에서의 input은 1개, output은 2개 hidden layer 수는 2개이다. 또한 각 노드의 Activation Function은 sigmoid function을 사용하고 bias는 제외하고 계산한다.

  ##### 초록색 값들은 초기에 주어진 값들이고($x_1$, weight), 파란색 값들은 이 값들을 바탕으로 계산한 값들이다.

  ##### 처음 값을 계산해보면 input 값은 0.5, $weight_{10}^{(0)}$은 0.15이기 때문에 이 둘을 곱한 0.075값이 나오게 된다.

  ##### 이 계산들을 통해 값을 계산하면 예측한 $y_1$의 값은 0.609이지만 실제 값은 0.3이고,  예측한 $y_2$의 값은 0.633이지만 실제 값은 0.9이다. 따라서 $y_1$의 값은 줄이도록 개선해야 하고, $y_2$의 값은 증가하는 방향으로 weight들을 변경해야 하는 것을 알 수 있다.

  ![image-20210402180709872](C:\Users\winner\AppData\Roaming\Typora\typora-user-images\image-20210402180709872.png)

  ##### Error를 측정하는 방식은 MSE 방식을 사용하였고, 그 결과 학습 전 전체 Error는 0.087인 것을 알 수 있다.

---



- ### 역전파

  ##### 역전파 알고리즘을 적용할 때 신경망의 weight들은 2분류로 구분할 수 있다. output으로부터 가장 가깝게 위치한 weight과 그 외의 weight들로 말이다. 우선 output으로부터 가장 가깝게 weight들의 역전파부터 살펴보면 아래와 같다.

  ![image-20210402180939610](C:\Users\winner\AppData\Roaming\Typora\typora-user-images\image-20210402180939610.png)

  ##### 전체 Error에 $w_{10}^{(1)}$이 미치는 영향은 전체 Error에 $w_{10}^{(1)}$으로 편미분을 함으로써 알 수 있다. 또한 이식을 풀어보면 위와 같이 3가지 식의 곱으로 나타낼 수 있다.

  ##### 각각 전체 error에는 $a_{20}$이 영향을 미치고 이 $a_{20}$에는 $z_{20}$이 영향을 미치고 또한 이 $z_{20}$에는 $w_{10}^{(1)}$이 영향을 미치는 것을 나타낸다.

  ##### 우선 1번째 식부터 계산하면 아래와 같다.

  #####  ![image-20210402181246515](C:\Users\winner\AppData\Roaming\Typora\typora-user-images\image-20210402181246515.png)

  ##### $E_{tot}$를 $a_{20}$에 대해서 편미분을 하면 위와 같은 식이 나온다. $target_{y1}$는 실제 값인 0.3을 의미하고, $a_{20}$은 이미 계산된 값인 0.609를 의미한다.

  ##### 계속해서 2번째 식을 계산해보면 아래와 같다.

  ![image-20210402181514311](C:\Users\winner\AppData\Roaming\Typora\typora-user-images\image-20210402181514311.png)

  ##### sigmoid function의 미분식은 위와 같고, $z_{20}$의 값을 넣어 계산해보면 쉽게 구할 수 있다.

  ##### 마지막 3번째 식을 계산해보면,

  ![image-20210402181639469](C:\Users\winner\AppData\Roaming\Typora\typora-user-images\image-20210402181639469.png)

  ##### $z_{20}$을 $w_{10}^{(1)}$에 대해서 편미분을 하게 되면 쉽게 $a_{10}$이 나온다는 것을 알 수 있고, 이 $a_{10}$의 값은 0.518로 이미 알고 있는 값이다.

  ##### 이 3가지 식의 값을 조합하면 $w_{10}^{(1)}$이 전체 error에 대해서 얼마나 영향을 미치는지 계산할 수 있다.

  ![image-20210402181908928](C:\Users\winner\AppData\Roaming\Typora\typora-user-images\image-20210402181908928.png)

  ##### 계산결과 0.0381이라는 값이 나왔다. 이 값을 학습시키기 위해 아래와 같이 계산한다.

  ![image-20210402182002822](C:\Users\winner\AppData\Roaming\Typora\typora-user-images\image-20210402182002822.png)

  ##### 이번에는 output으로부터 처음 등장하는 weight가 아닌 것에 대해서 알아본다. 이 2종류의 weight가 다른 이유는 output으로부터 처음 등장하는 weight는 하나의 output 값에만 영향을 미치지만, 나머지 weight들은 하나의 output만이 아니라 더 많은 output에 영향을 미치기 때문이다.

  ##### ![image-20210402182229670](C:\Users\winner\AppData\Roaming\Typora\typora-user-images\image-20210402182229670.png)

  ##### 위의 그림과 같이 $w_{10}^{(1)}$은 하나의 output인 $y_1$에 영향을 미치지만, output으로부터 처음 등장한 weight가 아닌 $w_{10}^{(0)}$은 2갈래로 나뉘어져 $y_1, y_2$에 영향을 미친다는 것을 알 수 있다.

  ##### 위의 식과 같이 전체 error에 $w_{10}^{(0)}$이 영향을 미치는 정도를 알아보기 위해서는 전체 error에 대해 $a_{10}$이, $a_{10}$에는 $z_{10}$이, $z_{10}$에는 $w_{10}^{(0)}$이 어떻게 영향을 미치는지 알아보면 된다.

  ##### 또한 전체 error는 $y_1$의 error, $y_2$의 error의 합으로 나타낼 수 있다.

  ![image-20210402183036101](C:\Users\winner\AppData\Roaming\Typora\typora-user-images\image-20210402183036101.png)

  ##### 이렇게 계산하면 $a_{10}$가 $E_1$에 미치는 영향을 알 수 있다. 여기서는 0.0294이다.

  ![image-20210402183338226](C:\Users\winner\AppData\Roaming\Typora\typora-user-images\image-20210402183338226.png)

  ##### 마찬가지로 $a_{10}$가 $E_2$에 미치는 영향도 알 수 있다. 여기서는 -0.0328이다.

  ##### 이 값들을 조합하면 전체 error에 $w_{10}^{(0)}$이 미치는 영향을 알 수 있다.

  ![image-20210402183459570](C:\Users\winner\AppData\Roaming\Typora\typora-user-images\image-20210402183459570.png)

  ##### 그 결과 -0.00042의 영향을 미쳤고, 학습된 값은 0.1502로 영향이 늘어나게 된것을 알 수있다.(기존 : 0.15, 학습 후 : 0.1502)

  ##### 전체적으로 학습 전과 학습 후를 보게되면 아래와 같다.

  ![image-20210402183705642](C:\Users\winner\AppData\Roaming\Typora\typora-user-images\image-20210402183705642.png)

  ##### 위의 값을 기준으로 학습 후 예측한 값들이 한층 원하는 값에 가까워졌다는 것을 알 수 있다.