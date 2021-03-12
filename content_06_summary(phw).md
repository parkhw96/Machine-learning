## Logistic Regression



- ### <u>classification</u>

  ##### y의 값이 별개의 값

  ##### classification problems에는 Email중 spam인지 아닌지, Tumor가 악성인지 양성인지, 등등과 같은 것들이 있다.

  ##### 이러한 문제들에서 변수는 Y이다. Y는 0또는 1이며 0은 negative class(어떤 것의 부재), 1은 positive class(어떤 것의 존재)이다.

  ##### 우선 binary class problems부터 보면, Tumor size vs malignancy를 예로 들 수 있다. 0과 1로 Malignant가 있는지 없는지로 표현한다.(있으면 1, 없으면 0)

  ##### 여기에서 linear regression을 아래와 같이 사용할 수 있다.

  ##### ![content_06(1)](img/content_06(1).PNG)

  ##### hypothesis의 결과값이 0.5(임계값, threshold)가 되는 곳에 수직으로 선을 긋고, 그 임계값에 해당하는 x의 값을 기준으로 output을 분류한다.(분홍점의 x좌표보다 큰 값이 들어오면 1로, 작은값이 들어오면 0으로)

  ##### 위의 작업은 합리적인 것처럼 보이지만, 만약 매우 Tumor size가 큰 하나의 yes가 들어온다고 하면, 그 data들에 맞는 가설함수(직선)를 다시 그리게 될것이다. 그렇게 되면 아래와 같이 파란색 직선이 생기고, 임계점에 해당하는 x의 값은 더 오른쪽으로 이동해 원치않는 방향으로 분류를 하게 된다.

  ##### ![content_06(2)](img/content_06(2).PNG)

  ##### 이러한 문제 말고도 linear regression에서 또다른 문제가 있다. Y가 0또는 1이라는 것을 알지만, linear regression에서의 hypothesis는 1보다 크거나 0보다 작은 값을 줄 수 있다라는 문제이다.

  ##### logistic regression은 항상 0또는 1인 값을 생성해내기 때문에 logistic regression은 classification algorithm이다.

---



- ### <u>Hypothesis representation</u>

  ##### classification에서의 hypothesis는 어떻게 표현할까?

  ##### linear regression에서의 hypothesis는 $h_\theta(x) = (\theta^Tx)$이다. 이와 다르게 classification hypothesis는 $h_\theta(x) = g((\theta^Tx))$로 표현한다. 

  ##### 여기서 $g(z) = 1 / (1 - e^{-z})$(z는 실수)로 정의되며, sigmoid function 혹은 logistic function으로 불린다. 이 식과 위의 hypothesis를 결합해보면 아래와 같은 결과가 나온다.

  ##### ![content_06(3)](img/content_06(3).PNG)

  ##### sigmoid function은 아래와 같이 생겼다.

  ##### ![content_06(4)](img/content_06(4).PNG)

  ##### 0.5를 통과하며 그 뒤로 평평 해진다.(0과 1에서의 점근선이 있다.)

  - #### <u>Interpreting hypothesis output</u>

    ##### hypothesis가 숫자를 출력할 때, 그 값을 input x가 들어왔을 때, y=1인 추정된 확률로 취급한다.

    ##### 예를 들어, $h_\theta(x) = 0.7$이라면, 그 환자는 종양이 악성(y=1)일 확률이 70%라는 의미이다. 이것을 기호로 쓰게 되면, $h_\theta(x) = P(y=1 |x; \theta)$로 쓸 수 있다. 이 의미는 x와 $\theta$가 주어졌을 때 y=1일 확률이라는 의미이다.

    ##### 위에서 봤듯이 종양이 악성인지 양성인지 분류하는 문제는 이진 분류 작업이기 때문에 y=0과 y=1밖에 없다. 따라서 $P(y=1 |x; \theta) + P(y=0 |x; \theta) = 1$이라는 식이 성립한다.

---



- ### <u>Decision boundary</u>

  ##### sigmoid function을 사용하는 한가지 방법에는 hypothesis의 출력 값이 0.5보다 크면 y=1로 예측하고, 그 외에는 y=0으로 예측한다라는 것이다.

  ##### 그렇다면 언제 $h_\theta(x)$가 정확히 0.5보다 크게 될까?

  ##### sigmoid function을 보게 되면

  ##### ![content_06(5)](img/content_06(5).PNG)

  ##### z가 0보다 크거나 같을 때, g(z)는 0.5보다 크거나 같게 된다. 따라서 z가 양수라면 g(z)는 0.5보다 크게 된다.

  ##### $z = (\theta^Tx)$이기 때문에 $\theta^Tx >= 0$일 때, $h_\theta(x) >= 0.5$가 된다.

  ##### 그러므로 $\theta^Tx >= 0$일 때, hypothesis는 y=1을 예측하고, $\theta^Tx <= 0$일 때, hypothesis는 y=0을 예측한다.

  - #### <u>Decision boundary</u>

    ##### $h_\theta(x) = g(\theta_0 + \theta_1{x_1} + \theta_2{x_2})$가 있다고 하자.

    ##### ![content_06(6)](img/content_06(6).PNG)

    ##### 예를 들어, $\theta_0 = -3, \theta_1 = 1, \theta_2 = 1$이라고 하면, $z = \theta^Tx$이기 때문에 parameter값들을 식에 대입해보면 $-3{x_0} + 1{x_1} + 1{x_2}$가 나오게 되고 그에 따라 $3{x_0} + 1{x_1} + 1{x_2} >= 0$일 때 y=1이라고 예측한다.

    ##### 다시 말해 $x_1 + x_2 >= 3$일 때, y=1이라고 예측한다는 것이다. $x_1 + x_2 = 3$을 그리게 되면 그것이 decision boundary가 된다.

    ##### ![content_06(7)](img/content_06(7).PNG)

    ##### 저 분홍직선이 decision boundary이고, 정확히 얘기하자면 저 decision boundary는 $h_\theta(x) = 0.5$일 때의 점들의 집합이다.

    ##### 데이터 없이 hypothesis와 parameter를 가지고 boundary를 만들 수 있다.

---



- ### <u>Non-linear decision boundaries</u>

  ##### $h_\theta(x) = g(\theta_0 + \theta_1{x_1} + \theta_2{x_2} + \theta_3{x_1^{2}} + \theta_4{x_2^{2}})$가 있다고 하자. 

  ##### $\theta^T$가 [-1, 0, 0, 1, 1]일 때, 즉 $-1 + {x_1}^2 + {x_2}^2 > = 0$일 때, y=1이라고 예측한다.

  ##### ${x_1}^2 + {x_2}^2 = 1$을 그려보면, 아래와 같이 반지름이 1인 원이 나오게 된다.

  ##### ![content_06(8)](img/content_06(8).PNG)

  ##### 더 고차다항식을 사용함으로써, 더 복잡한 decision boundaries를 얻을 수 있다.

---



- ### <u>Cost function for logistic regression</u>

  ##### parameter($\theta$)들을 적합시킨다.

  ##### linear regression에서는 $\theta$를 결정하기 위해 아래와 같은 cost function의 식을 썼다.

  ##### ![content_06(9)](img/content_06(9).PNG)

  ##### 이제는 squared error항 대신에, 'cost()'라는 것을 정의하게 된다.

  ##### ![content_06(10)](img/content_06(10).PNG)

  ##### linear regression에서 사용하던 것과 같은 측정을 사용하여 각각의 example에 대해 cost를 평가한다.

  ##### 다시 $J(\theta)$를 정의하게 되면 아래와 같다.

  ##### ![content_06(11)](img/content_06(11).PNG)

  ##### 모든 training data에 대한 개별적인 cost들의 합을 training data의 개수(m)으로 나눈 것이다.

  ##### 더 간단하게 하기 위해 윗첨자를 지울 수도 있다.

  ##### ![content_06(12)](img/content_06(12).PNG)

  ##### 이것이 의미하는 바는 결과가 $h_\theta(x)$이고 실제 결과가 y일 때, learning algorithm이 지불해야하는 비용이다.

  ##### 하지만 만일 위와 같은 함수를 logistic regression에 사용한다면 parameter $\theta$에 대해 non-convex function이다.

  ##### ![content_06(13)](img/content_06(13).PNG)

  ##### logistic regression에서의 hypothesis가 비선형 함수이고, 그 함수를 Cost()라는 함수에 넣고 또 그것을 cost function에 넣어 $J(\theta)$를 그리게 되면 왼쪽과 같은 그림이 나오게 된다.

  ##### non-convex라는 의미는 많은 local optimum이 있다는 것이고, gradient descent가 global optimum을 못 찾을 수 있다는 것이다.

  ##### 그래서 gradient descent가 global minimum에 수렴하기를 원한다면 convex function이어야 한다.

  - #### <u>A convex logistic regression cost function</u>

    ##### 이러한 것을 극복하기 위해 다른 것이 필요하다.

    ##### convex Cost() function이란, gradient descent를 적용시킬 수 있다는 의미이다.

    ##### ![content_06(14)](img/content_06(14).PNG)

    ##### 위의 식이 logistic regression에서의 Cost() function이다. 

    ##### y=1일 때를 그려보면 아래와 같다.

    ##### ![content_06(15)](img/content_06(15).PNG)

    ##### y=1이기 때문에 $-log(h_\theta(x))$를 사용한다.(x축은 $h_\theta(x)$(예측한 값), y축은 예측과 관련된 cost)

    ##### 올바르게 예측했을 때에는(1이라고 예측), Cost()의 값은 0이다.

    ##### 하지만 그렇지 않고 더 많이 잘못 예측할 수록 Cost()의 값은 서서히 증가한다.

    ##### 만약 hypothesis가 1을 예측하고 y=1이라면 정확히 예측한 것이 되기 때문에 Cost()의 값은 0이다. 그렇지 않고 hypothesis가 0쪽으로 가까워진다면 Cost()는 무한대로 간다.(잘못 예측한 것이기 때문에)

    ##### y=0일 때를 그려보면 아래와 같다.

    ##### ![content_06(16)](img/content_06(16).PNG)

    ##### y=0이기 때문에 $-log(1 - h_\theta(x))$를 사용한다.(x축은 $h_\theta(x)$(예측한 값), y축은 예측과 관련된 cost)

    ##### $h_\theta(x)$가 1에 가까워지면 Cost()는 무한대로 간다.(y=0인데 잘못 예측했기 때문에)

    ##### 이로써 cost function $J(\theta)$는 convex형태를 띄게 되고 local minimum을 피할 수 있다.

---



- ### <u>Simplified cost function and gradient descent</u>

  ##### logistic regression의 cost function은 다음과 같다.

  ##### ![content_06(17)](img/content_06(17).PNG)

  ##### 두 줄 혹은 두 가지 case로 적는 대신 한 개의 방정식으로 압축할 수 있다. 이렇게 압축하는 것이 더 효율적이다.

  ##### ![content_06(18)](img/content_06(18).PNG)

  ##### 각각 y=1, y=0을 대입해보면 위에서 보았던(2가지 case로 나누는 경우)것과 같은 것을 확인할 수 있다.

  ##### 따라서 $\theta$ parameter에 대한 cost function은 아래와 같다.

  ##### ![content_06(19)](img/content_06(19).PNG)

  - #### <u>How to minimize the logistic regression cost function</u>

    ##### $J(\theta)$를 최소화하는 방법 -> gradient descent를 사용한다.

    ##### ![content_06(20)](img/content_06(20).PNG)

    ##### 이 방정식은 linear regression에서의 규칙과 같지만, 다른 점은 hypothesis의 정의가 다르다는 것이다.

    ##### 즉, linear regression에서의 gradient descent와 흡사하다.

---



- ### <u>Advanced optimization</u>

  ##### logistic regression에 대해 cost function을 최소화하기 위해 gradient descent를 사용하는 것 대신에 Conjugate gradient, BFGS, L-BFGS를 사용할 수 있다.

  ##### 이러한 것들은 똑같은 입력을 받아 cost function을 최소화하는데 더 최적한 알고리즘들이며 또한 매우 복잡한 알고리즘들이다.

  ##### 장점에는 수작업으로 learning rate를 고를 필요가 없고, 종종 gradient descent보다 빠르다는 것이 있다.

  ##### 단점에는 debugging하는데 더 어렵다는 것 등등이 있다.

---



- ### <u>Multiclass classification problems</u>

  ##### Multiclass classification에 대해 logistic regression에서는 one vs. all를 사용한다.(하나 대 다수)

  ##### ![content_06(21)](img/content_06(21).PNG)

  ##### one vs. all classification을 사용하는 것은 multiclass classification을 binary classification처럼 만들어 준다.

  - #### <u>one vs. all classification</u>

    ##### 3가지 binary classification problems으로 training set을 나눈다.(즉, fake training set을 새롭게 만들어 계산한다)

    ##### ![content_06(22)](img/content_06(22).PNG)

    ##### 세모(클래스 1), 네모(클래스 2), 엑스(클래스 3)

    ##### 첫번째 예와 같이 네모와 엑스를 fake training set 동그라미로 둔다. 그리고 그에 적합한 hypothesis를 설정한다.($h_\theta^{(1)}(x)$) 세모는 positive class로 두고 나머지는 negative class로 둔다. 그렇게 학습시키면 분홍색 직선과 같은 경계선을 만들 수 있다.

    ##### 두번째 예와 세번째 예도 똑같이 적용한다.

    ##### ![content_06(23)](img/content_06(23).PNG)

    ##### 즉, 입력 x와 $\theta$가 주어졌을 때 y=i를 예측할 확률이다.

    ##### 새로운 입력 x값이 주어지면, 모든 hypothesis에 값을 넣어 가장 높은 확률이 나온 클래스를 고른다.

