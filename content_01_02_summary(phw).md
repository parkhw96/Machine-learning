## Machine learning에 대한 전반적인 개요

---



- ### <u>Several types of  learning algorithms</u>

  ##### Supervised learning : 컴퓨터에게 어떤 것을 하는 방법을 <u>가르친다</u>.

  ##### Unsupervised learning : 컴퓨터에게 어떤 것을 하는 방법을 <u>배우게 한다</u>.

  ##### Reinforcement learning

  ##### Recommender systems

---



- ### <u>Supervised learning</u>

  ##### Machine learning에서 가장 흔한 문제 타입이다.

  ##### 알고리즘에게 '정답'이라는 data set을 준다.

  ##### Supervised learning은 문제 타입에 따라 regression problem과 classification problem으로 나뉜다.

  ##### regression problem은 기대되는 값(output)이 <u>연속적</u>인 것이고 classification problem은 기대되는 값(output)이 <u>불연속적</u>인 것이다.

  ##### ex) Regression problem : housing price	Classification problem : Tumor size

---



- ### <u>Unsupervised learning</u>

  ##### '정답'을 주지 않는다. Unlabeled data를 준다.

  ##### Unsupervised learning을 하는 방법에는 data를 그룹으로 cluster하는 clustering algorithm과 cocktail party algorithm이 있다.

  ##### ex) Clustering algorithm : 유전정보	Cocktail party algorithm : 통화

---



- ### <u>Supervised learning과 Unsupervised learning의 차이</u>

  ##### Supervised learning : 컴퓨터에게 가르쳐야 한다. 정답을 준다. Labeled data(분류가 되어있는)를 준다.

  ##### Unsupervised learning : 컴퓨터에게 가르칠 필요가 없다.(스스로 배운다) 정답을 주지 않는다. Unlabeled data(분류가 되어있지 않은)를 준다.

---



- ### <u>Linear Regression</u>

  ##### m = 학습시킬 데이터의 수(training data set의 수)

  ##### 			x's = 입력 variables / features(입력 값)

  ##### 			y's = 출력 variable(목표 값)

  ##### 준비된 trainging set을 가지고 learning algorithm에 넣는다. 그러면 그 알고리즘은 hypothesis라는 함수를 출력해 낸다. 그러면 이 함수(hypothesis)는 입력을 가지고 Y라는 예측 값을 출력한다.

  ##### 전에 보았던 house price를 예를 들어 보면 hypothesis는 아래와 같은 형태로 표현된다. 

  $$
  h_\theta(x) = \theta_0 + \theta_1x
  $$

  ##### 간단하게 h(x)로도 표기한다.

  ##### $\theta_i$는 parameter이다. 

  ##### $\theta_0$는 zero condition, $\theta_1$는 기울기이다.

  ##### 위와 같은 함수(hypothesis)는 한 개의 variable을 가지고 있는 linear regression이다.

---



- ### <u>Linear regression - implementation(cost function)</u>

  ##### cost function은 데이터에 가장 잘맞는 직선이 무엇인지 알려준다. 

  ##### x값을 $h_\theta(x)$에 넣어 실제 y값과 근사한 출력 값을 얻어야 한다.

  ##### minimization problem -> Minimize $(h_\theta(x) - y)^2$ : $h_\theta(x)$과 y의 차이를 최소화 해야 한다.(각각, 모든 예제에 대해서 해야 한다.)

  ##### 그리고 다 더한다.

  $$
  \frac {1} {2m} \sum_{i=1}^m(h_\theta(x^i) - y^i)^2
  $$

  ##### 위의 식이 cost function이다.

  ##### 예측한 값과 실제 y값의 차이를 제곱한 것의 평균이 작은 것을 구해야 한다.

  ##### $\frac {1} {2m}$ : 평균이라고 하면 $\frac 1 m$을 사용해야 하지만 미분하기 쉽고 결과에 큰 영향을 주지 않기 때문에 $\frac {1} {2m}$을 사용한다.

  ##### 위와 같은 cost  function을 최소화하는 것이 목표이다.

  ##### 이러한 cost function은 또한 squared error cost function이라 불린다.

  ##### cost function은 $\theta$와 같은 parameter들을 결정한다.

  ##### 이러한 parameter들은 hypothesis가 어떻게 생겼는지, 어떻게 작동하는지 알려준다.

  ##### cost function을 쉽게 이해하기 위해 $\theta_0 = 0$으로 가정하고, hypothesis를 계산하면 다음과 같다.

  $$
  h_\theta(x) = \theta_1x \space(\theta_0 = 0)
  $$

  ##### 그렇게 되면 cost function은 다음과 같다.

  $$
  J(\theta_1) = \frac {1} {2m} \sum_{i=1}^m(h_\theta(x^i) - y^i)^2
  $$

  ##### 우리는 이 cost function을 최소화하는 $\theta_1$를 찾고 싶다.

  ##### 우선, 이 $h_\theta(x)$는 0, 0을 지나게 된다.

  ##### 예를 들어, 1) $\theta_1 = 1, J(\theta_1) = 0$ 2) $\theta_1 = 0.5, J(\theta_1) = ~0.58$ 3) $\theta_1 = 0, J(\theta_1) = ~2.3$이라고 하고, 이 값들을 $\theta_1$ vs $J(\theta_1)$을 그래프로 그리게 된다면 아래와 같은 그래프가 그려진다. 

  ##### ![content_01_02(1)](img/content_01_02(1).PNG)

  ##### learning algorithm에서 가장 중요한 목표는 $J(\theta_1)$을 최소화 시키는 $\theta_1$을 찾는 것인데, 그렇게 되면 여기서 최적의 $\theta_1$는 1이 된다.

---

- ### <u>A deeper insight into the cost function - simplified cost function</u>

  ##### 이번에는 $\theta_0$과 $\theta_1$ 두 개의 parameter가 있다고 하면($\theta_0 = 50, \theta_1 = 0.06$이라고 가정)

  ##### 그러면 아래와 같은 3차원 모양의 cost function의 그래프가 그려진다.($\theta_0, \theta_1, J(\theta_0, \theta_1)$의 그래프를 그려야 하기 때문에 x축, y축, z축이 필요하다)

  ##### ![content_01_02(2)](img/content_01_02(2).PNG)

  ##### 이 그림에서 y축은 cost function의 값을 나타내기 때문에 최소의 값을 알 수 있다.

  ##### 위와 같은 surface plot 대신에 contour figures/plot을 사용하면 아래 그림과 같다.

  ##### ![content_01_02(3)](img/content_01_02(3).PNG)

  ##### 각각의 색깔에 있는 점들은 $J(\theta_0, \theta_1)$의 값이 같지만, 명백하게 보자면 $\theta_0$과 $\theta_1$가 다르기 때문에 다른 위치에 있다.

  ##### 중앙에 근접할수록 좋은 hypothesis가 된다.

---

- ### <u>Gradient descent algorithm</u>

  ##### cost function J를 최소화할 때 사용한다.

  ##### parameter가 여러 개 있을 때에도 적용가능 하다.

  ##### ![content_01_02(4)](img/content_01_02(4).PNG)

  ##### := 의 의미는 업데이트 하겠다는 의미이다.

  ##### $\alpha$(alpha)의 의미는 학습 속도(learning rate)이다. alpha가 너무 작게 되면 조금씩 움직여 오래 걸리고, alpha가 너무 크면 최소값을 지나칠 수 있다. 따라서 alpha를 잘 고르는 것이 중요하다.

  ##### ![content_01_02(5)](img/content_01_02(5).PNG)

  ##### (for j =0 and j = 1)의 의미는 동시에 업데이트 하겠다는 의미이다. 동시에 업데이트를 하지 않게 되면 그것은 gradient descent가 아니고 이상하게 작동한다.(3차원의 공간이므로 따로 움직이는 것이 아니라 동시에 두 개의 점을 옮겨야 한다.)

  ![image-20210226165759412](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210226165759412.png)

  ##### 각각 $\theta_0$와 $\theta_1$에 대하여 편미분(partial derivative)을 하게 되면 위와 같은 식이 나오게 된다.

  ##### Linear regression cost function은 항상 convex function이다.(아래로 볼록한 모양) -> 따라서 gradient descent는 항상 global optima에 수렴할 것이다. linear regression cost function의 의미는 hypothesis가 1차 함수와 같은 것이다. 그렇게 되면 cost function의 그래프를 그리게 되면 2차 함수와 같이 나오게 된다.

---



- ### <u>summary</u>

  ##### 결국 $\theta_0$와 $\theta_1$가 gradient descent algorithm을 통해 최적의 수로 수렴하게 될 것이다. 그렇게 $\theta_0$과 $\theta_1$가 결정이 되면 hypothesis가 결정이 되고 내가 원하는 값(input)을 넣었을 때 그에 따른 결과 값(output)을 예측할 수 있게 된다.

---



- ### <u>sequence</u>

  ##### 1. 데이터를 보고(feature) 데이터의 성질에 따라 hypothesis를 결정 ex) $h_\theta(x) = \theta_0 + \theta_1x$

  ##### 2. $\theta_0$와 $\theta_1$을 임의의 값으로 설정, 초기에 0, 0과 같은 값으로 설정

  ##### 3. 그때의 cost function의 값을 계산

  ##### 4. 반복 횟수 만큼 gradient descent를 통해 $\theta_0$와 $\theta_1$의 값을 변경, 이때에도 매번 cost function의 값을 계산

  ##### 5. 반복 횟수 만큼 끝나게 되면 $\theta_0$와 $\theta_1$의 값이 어떠한 값으로 수렴할 수도 있다. 이 때의 값이 cost function을 최소화 하는 값일 수 있다. 만약 반복 횟수가 끝난 후 $\theta_0$와 $\theta_1$이 최적의 수로 정해졌다면

  ##### 6. 그 parameter들을 hypothesis에 대입해 값을 예측한다.

---



- ### <u>편미분 과정</u>

![image-20210225215549349](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210225215549349.png)
