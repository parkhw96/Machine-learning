## Linear Regression with Multiple Variables

---



- ### <u>Linear regression with multiple features</u>

  ##### Multiple variables = Multiple features(variable = feature = 변수)

  ##### n = number of features(변수의 수, x의 개수)

  ##### m = number of  examples(training data의 수)

  ##### $x^i$ = vector of the input for an example(training data에서의 i번째 데이터의 vector, feature들을 다 포함하고 있음), x는 n크기의 feature vector이다.

  ##### $x_j{^i}$ = i번째 training example에서의 j번째 feature의 값

  ##### 이전 hypothesis는 $h_\theta(x) = \theta_0 + \theta_1x$이다.(두 개의 parameter, 한 개의 variable(feature))

  ##### Multiple features(variables)일 때 hypothesis는 $h_\theta(x) = \theta_0 + \theta_1x_1 + \theta_2x_2 + \theta_3x_3 + \theta_4x_4$로 적을 수 있다.(parameter들은 여전히 cost function에 의해 결정된다.)

  ##### 표기의 편의상, $x_0 = 1$이라고 하면, 모든 example에 대해 0번째 feature($x_0 = 1$)를 추가로 가지게 된다. 그러면 feature vector는 인덱스가 0부터 시작하는 n+1 크기의 feature vector가 된다.(원래 크기가 n이었지만, $x_0$가 추가 되면서 크기가 하나가 늘어나게 됨) 이 $x_0$가 추가됨에 따라 새롭게 만들어진 example을 "X"라고 부른다.

  ##### parameter들 또한 인덱스가 0부터 시작하는 n+1크기의 벡터이다.(이러한 벡터는 $\theta$라고 불리는 column vector이다.)

  ##### 이로써, hypothesis는 $h_\theta(x) = \theta_0x_0 + \theta_1x_1 + \theta_2x_2 + \theta_3x_3 + \theta_4x_4$라고 할 수 있다.($x_0$가 추가됨)

  ##### $X = \begin{bmatrix} x_0 \\ x_1 \\ x_2 \\ x_3 \\ x_4 \end{bmatrix}$                              $\theta = \begin{bmatrix} \theta_0 \\ \theta_1 \\ \theta_2 \\ \theta_3 \\ \theta_4 \end{bmatrix}$                 $\theta^T = \begin{bmatrix} \theta_0 &\theta_1&\theta_2&\theta_3&\theta_4 \end{bmatrix}$

  ##### 위와 같이 X와 $\theta$가 되는데, $\theta$를 transpose해 곱연산을 하게 되면 $h_\theta(x) = \theta^TX$가 성립한다.

---



- ### <u>Gradient descent for multiple variables</u>

  ##### parameter들은 $\theta_0$부터 $\theta_n$까지 이다.(총 n+1개) 이 parameter들을 개별적인 값들로 생각하는 것 대신에 single vector($\theta$)로 생각한다.(여기서 $\theta$는 n+1 크기이다)

  $$
  J(\theta_0,\theta_1,...,\theta_n) = \frac {1} {2m} \sum_{i=1}^m(h_\theta(x^i) - y^i)^2
  $$

  ##### 위와 비슷하게, J(cost function)을 n+1개의 숫자들의 함수로 생각하는 것 대신에, parameter vector의 함수($J(\theta)$)라고 생각한다.

  ##### $ J(\theta_0,\theta_1,...,\theta_n) \to J(\theta)$

  ##### 이전에 배웠던, variable이 1개 일때, gradient descent의 공식은 아래와 같았다.

  ![image-20210226121303205](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210226121303205.png)

  ##### 위에서 보듯이 $\theta_0$와 $\theta_1$의 규칙(공식)이 다르다. 이것을 동일한 규칙(공식)으로 바꾸면 아래와 같다.

  ![image-20210226121354221](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210226121354221.png)

  ##### 즉, $\theta_j$ - learning rate(alpha) * ($\theta_j$에 대해 $\theta$ vector의 편미분)이다. $J(\theta)$를 parameter($\theta$) vector의 함수로 생각하기로 하였기 때문에 $\theta_j$에 대해 $\theta$ vector의 편미분을 한다.

---



- ### <u>Gradient Descent in practice: 1 Feature Scaling</u>

  ##### -Feature scaling

  ##### 	Multiple features에 대해 문제가 있다면 features들을 비슷한 규모로 만들어야 한다.(비슷한 규모로 만들	면 gradient descent가 더 빨리 원하는 값(global minimum)에 도달한다.)

  ##### 	예를 들어 x1 = size(0 - 2000 feet), x2 = number of bedrooms(1 - 5)이라면, $\theta_1$ vs $\theta_1$의 cost function 	그림을 그려보면 아래와 같이 길고 얇은 모양의 그림이 나오게 된다.(범위 차가 크게 남, cost function의 	gradient descent는 global minimum을 찾는 시간까지 오래 걸린다, 비효율적이다)

  ​	![image-20210226130645162](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210226130645162.png)

  ##### 	이러한 경우, input에 대해 rescale 하는 것이 더 효율적이다.

  ##### 	이것을 표준화를 한다면, $x_i$ <- ($x_i$ - mean) / max가 된다.

  ##### 	여기서  mean은 training set에서 $x_i$의 평균 값이다. max 대신 standard deviation(표준편차 혹은 max 	- min)으로 적어도 된다.

  ​	![image-20210226130936016](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210226130936016.png)

  ##### 	이렇게 되면 내가 가지고 있는 값들은 모두 대략 0이라는 평균을 가지게 된다.

---



- ### <u>Learning Rate $\alpha$</u>

  ##### ![image-20210226131034265](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210226131034265.png)

  ##### Gradient descent가 잘 작동 중이라면, $J(\theta)$는 매 반복마다 줄어 들게 된다.

  ##### 위에서 보다시피 특정 값 이후로는 큰 이득을 얻지 못한다.(iterations가 300 이후로는 큰 이득을 얻지 못한다.)

  ![image-20210226131135355](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210226131135355.png)

  ##### 이렇게 반복을 함에도 값이 증가하게 되면, $\alpha$를 줄여야 한다.

  ![image-20210226131202664](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210226131202664.png)

  ##### $\alpha$값을 줄이게 되면 green line처럼 minimum에 도달할 수 있다.

  ##### 혹여나 $J(\theta)$가 파도모양처럼 나온다면 더 작은 $\alpha$값이 필요하다.

  ##### $\alpha$값이 적당히 작다면 $J(\theta)$는 매 반복마다 줄어들 것이다. 하지만 $\alpha$값이 너무 작다면 $J(\theta)$가 줄어드는 속도가 매우 느릴 것이다.

---



- ### <u>Features and polynomial regression</u>

  ##### polynomial regression for non-linear function

  ##### Frontage($x_1$), Depth($x_2$) 2개의 features가 있다. 꼭 이 2개의 features들을 다 쓸 필요가 없다. 새로운 feature를 만들어 사용해도 된다. New feature(area, $x_3$) = frontage * depth. frontage와 depth는 house price를 예측하는데 중요한 feature가 아니다. area라는 feature가 중요한 feature가 된다.

  ##### 종종 이렇게 새로운 feature를 만드는 것이 더 좋은 model를 만들 수 있다.

  

  ##### - Polynomial regression

  ##### 	예를 들어, $\theta_0 + \theta_1x + \theta_2x^2$라는 quadratic function(2차 함수)가 있다. 이 함수를 housing data에 사용	할 수 있는데, 이는 별로 좋지 못하다. 굴절이 생기는 점이 있기 때문이다. 이 의미는 size가 엄청 커지면	 	housing  price는 감소한다는 의미이기 때문이다. 이 때문에 cubic function(3차 함수)를 사용하는 것이 	더 좋다.

  ​	![image-20210226131915153](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210226131915153.png)

  ##### 	기존 linear hypothesis와 cost function을 이러한 polynomial descriptions에 map하기 위해 가장 쉬	운 방법은 $x_1 = x, x_2 = x^2, x_3 = x^3$로 설정하는 것이다.

  ##### 	기존 polynomial 대신에 square root(제곱근), cubed root(세제곱근)과 같은 variable ^ (1 /                                              	something)을 사용할 수 있다.

---



- ### <u>Normal equation</u>

  ##### Normal equation은 몇몇 linear regression problems에 대해 더 좋은 해결책을 준다.

  ##### cost function을 $J(\theta) = a\theta^2 + b\theta + c$이라고 하면, 어떻게 최소화 시킬수 있을까?(여기서 $theta$는 vector가 아니라 real number, cost function은 quadratic function)

  ##### $\theta$에 대해 $J(\theta)$를 미분한다. 이제 그 미분한 것을 0과 같다고 둔다. 그렇게 되면 $J(\theta)$를 최소화하는 $\theta$의 값을 알 수 있다.

  ##### 그렇다면 원래의 cost function에서는 어떻게 최소화 시킬 수 있을까?(normal equation을 사용하여)

  ##### 우선 (모든 j에 대해)$\theta_j$에 대해 $J(\theta)$를 편미분하고 그 값을 0으로 둔다. 이 방법을 $\theta_0$부터 $\theta_j$까지 한다. 이렇게 되면 $J(\theta)$를 최소화하는 $\theta$값을 찾을 수 있다.

  ![image-20210226132705476](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210226132705476.png)

  ##### 여기서 m = 4(training data가 4개), n = 4(변수가 4개)

  ##### extra column을 추가한다.($x_0$ feature)

  ##### 추가된 data까지 포함된 [m x n+1] 크기의 matrix를 design matrix라고 한다.("X"라고 한다.)

  ##### y에 대해서도 비슷하게 한다면, [m x 1] 크기의 column vector y가 만들어 진다.

  ![image-20210226132842884](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210226132842884.png)

  ##### 이 식을 계산하게 되면 cost function을 최소화하는 $\theta$값을 찾을 수 있다.

  ##### 각 training example는 n+1크기의 feature column vector이다.

  ##### Design matrix(X)는 이러한 각 training example를 transpose하여 이어 붙여 만들어 진다.

  ![image-20210226133138200](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210226133138200.png)

  ##### 그 결과 X는 [m x n+1] 크기의 matrix가 된다.

  ##### Normal equation에서는 feature scaling할 필요가 없다.

  

##### 		- Gradient descent와 normal equation의 차이점	

| Gradient descent                       | Normal equation                     |
| -------------------------------------- | ----------------------------------- |
| Learning rate를 고를 필요가 있다.      | Learning rate를 고를 필요가 없다.   |
| 반복이 많이 필요함 $\to$ 오래 걸림     | 반복이 필요하지 않음                |
| n이 클 때 잘 작동한다.(n = feature 수) | n이 크면 느리다.                    |
| N이 10,000정도 이면 사용               | $(X^TX)^{-1}$를 계산할 필요가 있다. |

##### 	$(X^TX)$가 non-invertible이라는 것은 어떤 의미일까?

##### 		- Redundant features

##### 			feature들이 불필요하게 겹친다.

##### 			ex) $x_1$ = size in feet, $x_2$ = size in meters squared (둘이 같은 의미이다)

##### 		

##### 		- Too many features

##### 			m <= n (m = 10, n = 100)

##### 			때때로 작동하지만 항상 좋은 idea는 아니다.

##### 			Data가 부족하다.

##### 			이것을 해결하기 위해 1. feature를 삭제 2. regularization을 사용(적은 training set에 대해 많은 			         	        features들을 사용하게 해준다) 하는 방법이 있다.

