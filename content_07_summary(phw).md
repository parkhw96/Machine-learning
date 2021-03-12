## Regularization



- ### <u>The problem of overfitting</u>

  - #### <u>Overfitting with linear regression</u>

    ##### 우선 linear regression에서의 상황을 보게 되면, 데이터에 맞는 linear function은 좋지 않은 모델이다. 이러한 것은 underfitting이라고 하는데 또한 high bias(강한 편견, 강한 선입견)으로 불린다.

    ##### <u>bias : 모델에서 예측된 값과 실제값 사이 차이</u>

    ##### 2차 function에 맞추는 것은 더 잘 작동하는 것 같다.

    ##### 4차 다항식에 맞추는 것은 다섯개의 모든 example을 통해 곡석을 이룬다. training set에 대해 맞추는 것은 좋은 작업처럼 보이지만, 실제로는 좋은 model이 아니다. 이러한 것은 overfitting 또는 high variance라고 부른다.

    ##### <u>variance : 주어진 각 데이터에 해당하는 예측값들이 퍼져있는 정도</u>

    ![image-20210312150409966](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210312150409966.png)

    ##### 첫번째 그림에서 데이터(X)들이 hypothesis와 멀리 떨어져있으니 high bias인 것이고, 또한 예측값들이 파란색 선위에 있기 때문에 low variance이다.

    ##### 세번째 그림에서 예측값들이 구불구불한 선 위에 있으니(흩어져 있다) high variance이고, 또한 데이터(X)들이 hypothesis와 붙어있으므로 low bias이다. 

    ##### overfitting 문제는 feature가 너무 많아서 hypothesis가 training data set에 과적합할 때 발생한다.(위의 세번째 그림 참고) 이때의 비용함수는 거의 0이다. 따라서 training data set에는 완벽히 적합하지만 일반적인 해답을 제공하는데 실패한다. 이것은 generalize(일반화)가 가능하지 않다는 것이다.

  - #### <u>Overfitting with logistic regression</u>

    ##### logistic regression에서도 똑같은 일이 일어난다.

    ![image-20210312153026305](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210312153026305.png)

  ##### 만일 많은 feature들과 적은 data들을 가지고 있다면 overfitting이라는 문제가 생길 수 있다.

  ##### 이럴 때에는, feature의 수를 줄인다. 수작업으로 남길 feature들을 선택할 수도 있고, algorithm을 사용할 수 있다. Feature의 수를 줄이면서 정보도 같이 잃을 수 있기 때문에, data의 손실을 최소화 할 수 있는 feature를 골라야 한다.

  ##### 또 다른 방법으로는 Regularization이 있다. 모든 feature들을 남기되 parameter $\theta$의 규모를 줄이는 것이다. 이 regularization은 feature의 수가 많고 이 feature 각각이 y를 예측하는데 조금씩 기여한다면 그 때 잘 작동한다.

---



- ### <u>Cost function optimization for regularization</u>

  ##### 위의 linear regression에서 overfitting한 문제를 예로 들면, 그 overfitting을 피하기 위해 $\theta_3$와 $\theta_4$를 정말 작게 만드는 penalty를 준다.

  ![image-20210312153745172](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210312153745172.png)

  ##### 위의 파란색은 $\theta_3$와 $\theta_4$를 penalize(처벌)하기 위해 기존의 cost function을 수정한 것이다.

  ##### $\theta_3$와 $\theta_4$는 거의 0에 가까울 것이다. 앞에 붙어있는 상수가 매우 크기 때문에 cost function을 최소화하기 위해서는 $\theta_3$와 $\theta_4$는 0에 가까워야 할 것이기 때문이다.

  ##### 그렇게 되면 아래와 같이 아까 구불구불한 4차함수에서 2차함수로 바뀌게 된다.

  ![image-20210312154007351](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210312154007351.png)

  ##### 위의 예에서는 두 parameter 값에 패널티를 주었다.

  ##### regularization은 특정 parameter에 매우 작은 값을 부여하여 hypothesis를 단순화한다. 단순한 hypothesis는 덜 overfitting된다.

  ##### 만약 $x_1, x_2, ..., x_{100}$의 feature들을 가지고 있고 고차항이 무엇인지 모를 때 어떤 parameter를 선택하여 작은 값을 부여해야 할까?

  ##### 일반적으로 regularization을 통해 cost function을 가지고 모든 parameter들을 줄이도록 수정을 한다. 이때 마지막에 항을 하나 추가하게 되는데 이것을 regularization항이라고 한다. 이 regularization 항은 모든 parameter들을 줄인다.($\theta_0$는 제외하고, $\theta_1$부터 패널티를 부여한다)

  ##### regularization 항을 포함한 linear regression에서의 cost function은 아래와 같다.

  ![image-20210312154735599](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210312154735599.png)

  ##### cost function에 정규화 항을 포함시킴으로써, 데이터에 맞는 더 완만한 곡선과 더 좋은 hypothesis를 얻을 수 있다.

  ##### 만약 lamda가 매우 크다면, $\theta_0$를 제외한 모든 parameter들은 높은 패널티를 받아 거의 0으로 될 것이다. 만약 그런 일이 발생한다면 hypothesis에서 모든 항을 제거해버린 것과 같을 것이다. 그렇게 되면 underfitting이라는 결과가 나온다.

  ![image-20210312155127791](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210312155127791.png)

  ##### 그래서 lamda를 잘 선택해야 한다.

---



- ### <u>Regularized linear regression</u>

  ##### regularization을 적용한 linear regression의 cost function은 아래와 같다.

  ![image-20210312155250211](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210312155250211.png)

  ##### regularization에 대해 $\theta_0$에 패널티를 주지 않기 때문에 gradient descent 공식은 2가지로 나누어 구분한다.

  ![image-20210312155431289](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210312155431289.png)

  ![image-20210312155448194](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210312155448194.png)

  ##### 최종적으로 정리해보자면 아래와 같다.

  ![image-20210312155713040](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210312155713040.png)

  ##### $(1 - \alpha\frac {lamda} {m})$항은 대게 1보다 작다. 왜냐하면 learning rate는 작고, m은 크기 때문이다. 그래서 1 - (작은 숫자)로 된다. 따라서 이 항은 종종 0.95에서 0.99사이 이다.

  ##### 위와 같은 이유로 $\theta_j$는 더 작아진다.($\theta_j * 0.99$정도로 생각하면 됨)

---



- ### <u>Regularization with the normal equation</u>

  ##### normal equation은 linear regression의 다른 모델이다.

  ##### regularization을 사용하기 위해서 방정식에 (lamda[n+1 x n+1])의 항을 추가한다.

  ![image-20210312160416540](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210312160416540.png)

  - #### <u>Regularization for logistic regression</u>

    ##### logistic regression에서의 cost function은 아래와 같다.

    ![image-20210312160600032](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210312160600032.png)

    ##### 이제 여기에 regularization을 위해 아래와 같은 항을 추가한다.

    ![image-20210312160750704](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210312160750704.png)

    ##### 이것은 $\theta_1, \theta_2 ,..., \theta_n$까지 패널티를 주는 효과를 가진다. linear regression과 마찬가지로 더 적합한 저차항의 hypothesis를 가질 수 있다.(패널티를 줘서 항의 규모를 줄인다.)

    ##### 최종적으로는 아래와 같다.

    ![image-20210312160823613](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210312160823613.png)

    ##### regularization된 logistic regression의 gradient descent는 linear regression의 gradient descent와 hypothesis가 다르다는 점만 제외하면 똑같이 생겼다.

