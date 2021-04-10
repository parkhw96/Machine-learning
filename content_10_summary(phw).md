## Advice for applying Machine Learning



- ### Deciding what to try next

  ##### 만약 집 가격을 예측하기 위해 regularized linear regression을 사용했다면, 아래와 같은 cost function을 줄이도록 학습시킬 것이다.

  ##### ![content_10(1)](img/content_10(1).PNG)

  ##### 하지만 학습 시킨 후 새로운 데이터를 넣어 테스트를 해봤는데, 큰 에러가 나오게 된다면 어떻게 해야할까?

  ##### training data를 더 많이 수집하기, features의 수를 줄이기, 추가하기, $\lambda$를 낮추거나 올리기와 같은 방식을 사용할 수 있다.

---



- ### Evaluating a hypothesis

  ##### training data에 parameter들을 맞추기 위해  error를 최소화하는 쪽으로 시도할 것이다. 하지만 low error라고하는 것이 좋은 parameter이라고 할 수 없다.  왜냐하면 overfitting을 의미할 수도 있기 때문이다. 

  ##### 그렇다면 hypothesis가 overfitting이라는 것을 어떻게 알 수 있을까? 우선, hypothesis를 그리는 방법이 있다. 하지만 이러한 방법은 feature의 갯수가 많으면 불가능하다.

  ##### 그다음 방법으로는 data를 2부분으로 나누는 방법이 있다. 첫번째 부분은 training set, 2번째 부분은 test set과 같이 70:30 비율로 나눈다.

  ##### ![content_10(2)](img/content_10(2).PNG)

  ##### 그리고 이렇게 나눈 데이터를 학습시킨다.

  ##### training data로부터 parameter를 학습시키기 위해, 70%의 training set을 사용해 cost function을 최소화 시킨다. 그리고 test set으로부터 아래의 계산을 한다.

  ##### ![content_10(3)](img/content_10(3).PNG)

  ##### logistic regression도 똑같이 70%의 데이터로 학습시키고, 남은 30%로 test를 한다.

---



- ### Model selection and training validation test sets

  ##### training set을 2부분으로 나누는 대신 3부분으로 나눈다.

  ##### training set, cross validation set, test set으로 60:20:20의 비율로 나눈다.

  ##### ![content_10(4)](img/content_10(4).PNG)

  ##### 그렇다면 아래와 같이 차수를 고르는 문제에서 어떻게 적용시킬까?

  ##### ![content_10(5)](img/content_10(5).PNG)

  ##### 우선, training set으로 cost function을 최소화 시키는 parameter들을 찾으면 hypothesis가 결정된다. 이 hypothesis를 cross validation set을 통해 cross validation error를 계산한다. 이렇게 하게되면 1~10번까지의 각각 error들이 계산되는데 그 중 가장 작은 error를 발생시킨 model를 선택한다. 만약 5번이 선택 되었다면 마지막으로 test set을 통해 error를 측정한다. (test set error가 작을 수록 일반화를 잘시킨다는 의미)

---



- ### Diagnosis - bias vs. variance

  ##### 대게 안좋은 결과가 나오면 원인이 high bias와 high variance중 하나이다.

  ##### high bias는 underfitting문제이고, high variance는 overfitting문제이다.

  ##### ![content_10(6)](img/content_10(6).PNG)

  ##### ![content_10(7)](img/content_10(7).PNG)

  ##### 위 그림을 보면  차수가 높아질수록 overfitting쪽으로 된다는 것을 알 수 있다. 또한 두개의 error를 최소화 시키고 싶을 때는 d=2일때가 적당하다는 것을 알 수 있다.

  ##### 만일 d(차수)가 매우 작으면, high bias 문제가 생기고, d가 매우 크면 high variance 문제가 생긴다.

  ##### high bias에서, cross validation과 training error가 둘 다 높은 것을 알 수 있다. 이것은 training data도 잘 못 맞춘다는 것 뿐만 아니라 일반화도 잘 못한다는 것을 의미한다.

  ##### high variance에서, training error는 낮지만, cross validation은 높은 것을 알 수 있다. 이것은 training set에는 잘 맞추지만 일반화는 잘 못한다는 것을 의미한다.

---



- ### Regularization and bias/variance

  ##### ![content_10(8)](img/content_10(8).PNG)

  ##### 위 방정식은 regularization을 통해 높은 차수의 다항식을 fitting하는 것이다.

  ##### 여기서 만약 $\lambda$가 크다면 모든 parameter값에 크게 처벌해주는 것이고, 결국 parameter들은 0가 될 것이다. 또한 parameter들이 0에 가까운 값이 되기 때문에 hypothesis도 거의 0에 가까운 것을 갖게 될것이다. 그래서 high bias(underfitting)문제가 생긴다.

  ##### $\lambda$가 매우 작다면, 정규화항은 거의 0일것이고, high variance(overfitting)문제가 생긴다. 왜냐하면 hypothesis는 고차항이고 정규화항은 거의 0의 값이기 때문이다.

  ##### ![content_10(9)](img/content_10(9).PNG)

  ##### $\lambda$를 선택하는 방법은 $\lambda$를 0, 0.01, 0.02, 0.04, ..., 10까지 나누고 이 값들에 대해 각각 정규화항이 있는 cost function을 적용한다. 그렇게 되면 $\lambda$들에 대해 각각 parameter들이 나오게 되고, 이 parameter들을 cross validation error(정규화항이 없음)을 통해 가장 error가 적게 나온 parameter를 고르고, 이 parameter를 마지막으로 test set을 통해 일반화를 잘하는지 테스트를 한다.

---



- ### Learning curves

  ##### ![content_10(10)](img/content_10(10).PNG)

  ##### high bias일때에는 m이 클때에 두 곡선의 사이가 작기 때문에(error가 크게 유지됨), 더 많은 데이터는 도움이 되지 않는다.

  ##### ![content_10(11)](img/content_10(11).PNG)

  ##### high variance일때에는 m이 커지면 커질 수록 두 곡선의 사이가 작아지기 때문에(error가 작게 유지됨), 더 많은 데이터는 도움이 된다.

