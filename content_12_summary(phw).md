## Support Vector Machines(SVMs)



- ### An alternative view of logistic regression

  ##### 기존의 logistic regression의 하나의 example에 대한 cost function은 아래와 같다.

  ##### ![content_12(1)](img/content_12(1).PNG)

  ##### 이 식에 $h_\theta(x)$대신에 $h_\theta(x)$의 정의를 대신해 적어주게 되면 아래와 같은 확장된 cost function 방정식을 얻을 수 있다.

  ##### ![content_12(2)](img/content_12(2).PNG)

  ##### 만약 y = 1이라면 첫번째 항만이 남게되고 이것을 그래프로 그리게 된다면 아래와 같다.

  ##### ![content_12(3)](img/content_12(3).PNG)

  ##### 위 그래프를 보게 되면 z가 크다면 cost는 적은 것을 볼 수 있다. 하지만 z가 0또는 음수라면 cost는 큰 것을 볼 수 있다. 

  ##### 이와 마찬가지로 y = 0이라면 두번째 항만이 남게되고 z가 작다면 cost는 적은 것을 알 수 있다.

  ##### ![content_12(4)](img/content_12(4).PNG)

  ##### SVM에서는 위의 비용함수들을 조금씩 수정한다.

  ##### ![content_12(5)](img/content_12(5).PNG)

  ##### 위의 그래프가 새로운 y = 1일때의 cost function이다. 이러한 cost function은 계산적 이점과 최적화 문제를 더 쉽게 해결할 수 있게 한다. 또한 이러한 함수를 $cost_1(z)$라고 부른다.

  ##### ![content_12(6)](img/content_12(6).PNG)

  ##### 위의 그래프는 y = 0일때의 cost function이다. 또한 이러한 함수를 $cost_0(z)$라고 부른다.

  ##### ![content_12(7)](img/content_12(7).PNG)

  ##### 위의 식에서 아래와 식과 같이 변하게 된다.

  ##### ![content_12(8)](img/content_12(8).PNG)

  ##### 이제 여기서 조금 더 식을 변형하게 되는데, 우선 1/m을 없앤다. 1/m은 상수이기 때문에 최소화 문제를 1/m을 곱하던 나누던 $\theta$의 최소값은 동일하다. 예를 들어 (u-5)^2+1을 최소화하는 u의 값은 5이다. 또한 (u-5)^2+1) * 10을 하여도 최소화하는 u의 값은 5로 동일하다. 즉, m(상수)이 있으나 없으나 $\theta$을 최소화하는 값은 동일하기 때문에 1/m을 없앤다.

  ##### logistic regression에서 2개의 항이 있는데 Training data set 항을 A, Regularization 항을 B라고 한다면 A + $\lambda$B라고 적을 수 있다. 하지만 SVM에서는 편의를 위해 $\lambda$를 제거하고 CA + B의 꼴로 적는다. (C = $1 / \lambda$)

  ##### 아래와 같은 결과의 식이 나오게 된다.

  ##### ![content_12(9)](img/content_12(9).PNG)

---



- ### Large margin intuition

  ##### SVM은 large margin classifiers라고 불리는데 그 이유를 알아보겠다.

  ##### ![content_12(10)](img/content_12(10).PNG)

  ##### 만약 C가 매우 크다면 (ex : 100,000) CA + B를 최소화 하기 위해서 A는 0이 될것이다. A를 0으로 만들기 위해서는 y = 1일때에는 $\theta^T{x}$가 1보다 크거나 같을것이고, y = 0일때에는 $\theta^T{x}$가 -1보다 작거나 같을 것이다. CA가 0이 되기 때문에 B를 최소화하는 것으로 된다.

  ##### ![content_12(11)](img/content_12(11).PNG)

  ##### 즉, 위와 같이 B의 항을 최소화 하는 것이 남게 된다.

  ##### ![content_12(12)](img/content_12(12).PNG)
  
  ##### 위의 그림과 같이 decision boundaries를 생각해보면 초록색 선과 분홍색 선을 보면 좋아 보이지 않는다.
  
  ##### SVM은 검은색 선을 decision boundaries로 선택한다. 검은색 선은 positive 예제와 negative 예제를 더 잘 구분한다. 검은색 선은 training example로부터 더 큰 minimum distance(margin)을 가진다. 즉, 파란색선과 검은색 선 사이가 margin이다. 그러므로 SVM을 large margin classifier라고 부른다.
  
  ##### ![content_12(20)](img/content_12(20).PNG)
  
  ##### C가 매우 크다면 decision boundary는 검은색 선에서 보라색 선으로 움직이며, C가 적당히 작다면 decision boundry는 검은색 선이다. 즉, C가 적당하다면 SVM은 비선형적으로 분리된 데이터든(동그라미 사이에 엑스 데이터가 들어있는 경우), 위와 같이 하나의 example이 떨어져 있는 경우에도 large margin으로 example들을 분리한다.

---



- ### Kernels - 1: Adapting SVM to non-linear classifiers

  ##### ![content_12(13)](img/content_12(13).PNG)

  ##### 다항식을 표현하는 또 다른 방법이 있는데, f1, f2, f3, f4 등등의 새로운 feature들을 사용하여 표현할 수 있다. 예를 들어 y = 1를 예측하는것을 다른 방법으로 표현해보면 아래와 같다.

  ##### ![content_12(14)](img/content_12(14).PNG)

  ##### 위와 같이 f들을 정의하는 것 대신 다른 방법이 있다.

  ##### ![content_12(15)](img/content_12(15).PNG)

  ##### l1, l2, l3는 랜드마크라 한다. 

  ##### ![content_12(16)](img/content_12(16).PNG)

  ##### f1은 학습 예제 x가 l1와 얼마나 유사한지 또는 가까운지를 정의하는 similarity function이다.

  ##### f2와 f3도 이와같이 정의할 수 있고, 이러한 similarity function을 kernel이라고 한다.

  ##### similarity 대신에 k를 사용하여 표현하기도 한다.

  ##### 만약 위의 식에서 학습예제가 x가 랜드마크에 가깝다고 한다면 분자는 0에 가까울 것이며 따라서 exp^0은 1이 되게 된다. 즉, x가 랜드마크에 가까울수록 f의 값은 1에 가까워 진다. 반대로 x가 랜드마크에서 멀어질수록 f의 값은 0에 가까워진다. 

  ##### 즉, kernel은 x(학습 예제)가 랜드마크와 얼마나 가까운지 또는 얼마나 유사한지를 측정한다. f는 학습 예제 x가 랜드마크에 가까울수록 1에 가까워지고, 멀어질수록 0에 가까워진다.

  ##### 이러한 similarity function을 Gaussian Kernel이라 한다.

  ##### ![content_12(17)](img/content_12(17).PNG)

  ##### f1의 분모에 있는 것이 바뀜에 따라 모양도 변한다. 분모가 0.5일 때 f1은 [3,5]에서 움직이면 빠르게 0으로 떨어지고, 3일때에는 느리게 0으로 떨어진다.

  ##### ![content_12(18)](img/content_12(18).PNG)
  
  ##### 위와 같이 분홍색 점은 l1에 가깝기 때문에 1로, l2와 l3에는 멀기 때문에 0이 된다. 이제 이 값들을 넣어 계산하게 되면 0.8가 나오게 되어 0보다 크기 때문에 1로 예측한다. 반면에 하늘색 점은 모든 랜드마크와 멀기 때문에 0이 되고 이 값들을 넣어 계산하게 되면 -0.5가 된다. 따라서 0보다 작기 때문에 0으로 예측한다.
  
  ##### 결과적으로 빨간색 선의 decision boundry가 나온다. 즉, l1과 l2 근처의 점은 positive example이라고 예측하고 l1과 l2에서 멀리 떨어진 점들은 negative example이라고 예측한다. 
  
  ##### 즉, 고차다항식말고 landmark와 kernel을 사용하여 non-linear Decision boundry를 설정할 수 있다.

---



- ### Kernels 2

  ##### 그렇다면 landmark는 어떻게 설정해야 할까?

  ##### 학습 예제마다 똑같은 위치에 랜드마크를 배치한다. 그렇다면 m개의 랜드마크를 배치하게 된다. 즉, l1, l2, ..., lm으로 배치한다.

  ##### ![content_12(21)](img/content_12(21).PNG)

  ##### 이제 새로운 예제가 들어오게 되면 f0부터 fm까지의 값들을 모두 계산할 수 있다. (f0는 항상 1)

  ##### 이제 feature x를 feature f로 대체하기 위해서 아래와 같이 계산한다. 다시 말하면 (x^i, y^i)의 예제가 있다면, x^i는 아래와 같이 계산될 수 있다.
  
  ##### ![content_12(19)](img/content_12(19).PNG)
  
  ##### 그러므로 이러한 값들을 [m+1 x 1] 차원의 벡터 f로 그룹화 할 수 있다. f^i는 i번째 example에 대한 f 벡터이다.
  
  ##### 이러한 방법으로 x대신 f를 사용한다.
  
  ##### ![content_12(23)](img/content_12(23).PNG)
  
  ##### 위와 같이 f가 m+1차원으로 변경되었기 때문에, $\theta$도 m+1차원이다.
  
  ##### ![content_12(22)](img/content_12(22).PNG)
  
  ##### 정규화항도 n이 아닌 m으로 변경된다.
  
  ##### C가 크다면 $\lambda$가 작은 것과 동일하며 low bias, high variance이며 overfitting하기 쉽다.
  
  ##### 반대로 C가 작다면 $\lambda$가 큰 것과 동일하며 high bias, low variance이며 undergitting하기 쉽다.

---



- ### SVM - implementation and use

  ##### SVM을 사용하기 위한 많은 라이브러리와 패키지가 있기 때문에 직접 구현할 필요는 없다.

  ##### 하지만 이러한 라이브러리를 사용하기 위해서는 C를 선택하는 것과, 어떠한 kerel을 사용할지 선택해야 한다.

  ##### 위에서 언급한 Gaussian kernel 말고 linear kernel, string kernel, chi-square kernel, ... 등등이 있다.

  ##### linear kernel과 Gaussian kernel이 대표적이며 나머지 kernel들을 잘 사용되지 않는다.

---



- ### Logistic Regression vs. SVM

  ##### n이 크고 m이 적을 때에는 logistic regression 또는 linear kernel을 사용하는 SVM을 사용한다.

  ##### n이 작고 m이 중간정도라면 Gaussian kernel을 사용하는 SVM을 사용한다.

  ##### n이 작고, m이 크다면 feature들을 더 추가하고, logistic regression 또는 linear kernel을 사용하는 SVM을 사용한다.

  ##### Neural Network는 모든 경우에서 잘 작동하지만, 학습 속도는 느릴 수 있다.
