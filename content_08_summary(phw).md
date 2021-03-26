## Neural Networks - Representation



- ### Artificial neural network - representation of a neurone

  ##### ![content_08(1)](img/content_08(1).PNG)

  ##### 이 그림에서 neurone은 logistic unit(논리 유닛)이다. input wire들을 통해 입력을 받으며, logistic unit은 계산을 한다. 그리고 output wire들을 통해 output을 보낸다.

  ##### $x_0$는 bias unit으로 1이다.

  ##### $\theta$ vector는 모델의 가중치라고도 불린다.

  ##### 위의 그림은 한 개의 neurone만 가지고 있는 것을 표현한 것이고, 아래와 같이 neurone을 그룹으로 묶어 신경망을 만들 수 있다.

  ##### ![content_08(2)](img/content_08(2).PNG)

  ##### 여기에서 input은 $x_1, x_2, x_3$이다. 또한 첫번째 layer의 input activation이라고도 부른다.($a_1^{1}, a_2^{1}, a_3^{1}$)

  ##### 2번째 layer에는 $a_1^{2}, a_2^{2}, a_3^{2}$과 같이 3개의 neurone들이 있다.

  ##### 마지막 3번째 layer은 output 생성한다. 그 neurone을 $a_1^{3}$라고 부른다.

  ##### 다시 말하면, 첫번째 layer은 input layer이고, 마지막 layer는 output layer이다. 그 마지막 layer에서는 hypothesis에 의해 계산된 값을 만들어 낸다.

  ##### 중간에 있는 layer는 hidden layer이다. hidden layer에서는 값들이 어떻게 처리되는지 관찰하지 못한다. 또한 하나의 hidden layer말고 여러 개의 hidden layer를 가질 수 있다.

---



- ### Neural networks - notation

  ##### $a_i^{j}$ - j번째 layer에서 i번째 unit의 activation 함수를 거쳐 나온 값을 의미한다.

  ##### 그러므로 $a_1^{2}$는 2번째 layer에서 1번째 unit의 activation 함수를 거쳐 나온 값이다.

  ##### 즉, unit의 activation 함수는 그 unit에서 계산되고 출력된 값을 의미한다.

  ##### $\Theta^{(j)}$ - j번째 layer에서 j+1 layer까지 mapping하는 함수를 조절하는 가중치의 행렬을 의미한다.

  ##### $s_j$는 j번째 layer에서의 unit의 수를 의미한다.

  ##### 만약 layer j에 $s_j$이고, layer j+1에 $s_{j+1}$이라면 $\Theta^j$는 [$s_{j+1}$ x $s_j$ + 1] 크기의 행렬이다. 왜냐하면 mapping을 해야하기 때문에 현재 위치하고 있는 layer의 다음 layer인 layer j+1에서의 $s_{j+1}$과 현재  위치하고 있는 layer인 layer j에서 bias unit을 포함하기 때문에 $s_j$ + 1이 된다.

  ##### 예를 들면, 각각 101과 21개의 unit들을 가지고 있다고 하면 그 사이에 있는 $\Theta$ 행렬의 크기는 [21 x 102]가 된다.

  ##### 계산은 어떻게 이루어 질까? 우선, 각각의 node에 대해 activation 함수를 계산하는데 그 activation은 그 node에 대한 input과 parameter에 대해 달려 있다.

  ##### ![content_08(3)](img/content_08(3).PNG)

  ##### layer 2에 있는 activation들을 bias term과 input 값들에 기반해 계산한다.

  ##### 그리고 마지막 layer 3에 있는 hypothesis를 계산하는데, 여기에도 똑같은 논리가 적용되지만 다만 input이 x 값들이 아니라 이전 layer로부터의 activation 값들이다.

  ##### 여기에서 $\Theta^{(1)}$은 [3 x 4] 크기의 행렬이고, $\Theta^{(2)}$는 [1 x 4]의 행렬이다.

  ##### 모든 input과 activation은 다음 layer에서의 모든 node들에게 주어진다.(계산할 때 다 계산해야함)

  ##### $\Theta_{ji}^{l}$ - j는 다음 layer의 어느 node로 mapping 하는지, i는 현재 layer의 어느 node로부터 mapping 하는지, l은 어느 layer로부터 mapping하는지를 의미한다.

  ##### 예를 들면, $\Theta_{13}^{1}$는 다음 layer의 1번째 node로 mapping하고, 현재 layer의 3번째 node로부터 mapping 되며, layer 1로부터 mapping을 하는 것을 의미한다.

---



- ### Model representation 2

  ##### 이 부분에서는 계산을 효율적으로 하기 위해 vectorized 구현하는 방법을 알아본다.

  ##### ![content_08(4)](img/content_08(4).PNG)

  ##### 위에서 보았던 것과 같은 그림이 있다.

  ##### 여기에서는 새롭게 몇가지 것들을 정의한다.

  ##### $z_1^{2} = \Theta_{10}^{1}x_0 + \Theta_{11}^{1}x_1 + \Theta_{12}^{1}x_2+ \Theta_{13}^{1}x_3$로 정의한다. 이렇게 정의하면 $a_1^{2} = g(z_1^{2})$가 된다. 여기에서의 윗첨자는 해당되는 layer와 관계가 있다.

  ##### 위와 똑같이 $z_2^{2}, z_3^{3}$도 정의할 수 있다.

  ##### ![content_08(5)](img/content_08(5).PNG)

  ##### 이렇게 되면 다음과 같은 절차로 neural network의 계산을 벡터화할 수 있다.

  ##### $z^2 = \Theta^{(1)}x$ - $\Theta^{1}$은 [3 x 4] 크기의 행렬이고, x는 [4 x 1] 크기의 벡터이다. 그러므로 $z^2$는 [3 x 1] 크기의 벡터가 나온다.

  ##### $a^2 = g(z^{(2)})$는 $z^2$가 [3 x 1] 크기의 벡터이므로, $a^2$도 당연히 [3 x 1] 크기의 벡터이다. $a^2$는 $z^2$의 각 요소에 대해 sigmoid(logistic) 함수를 적용하는 것으로 계산된다.

  ##### input layer에게도 notation을 단일화 하게 되면, $a^1 = x$로 표기할 수 있다.

  ##### 이렇게 표기하게 되면 $a^1$은 input vector이고, $a^2$는 $g(z^2)$에 의해 계산된 값들의 vector이다.

  ##### ![content_08(6)](img/content_08(6).PNG)

  ##### 이렇게 마지막 hypothesis를 계산할 때 $a_0^{2}$가 필요하다. 이것은 앞서 말했듯이 bias unit으로 1이다. hypothesis를 계산하기 위해서 $a^2$를 [3 x 1] 크기의 벡터에서 $a_0^{2}$를 더해 [4 x 1] 크기의 벡터로 만든다.

  ##### $z^3 = \Theta^{2} a^2$가 위와 같은 방식으로 계산되고, $h_\Theta(x) = a^3 = g(z^3)$이 된다.

  ##### 이러한 처리과정을 forward propagation이라고 한다. 즉, input unit으로 부터 시작해 각각의 layer들의 값(activation 함수를 적용해 나온 값)을 forward propagate하고 계산한다.

  ##### 위와 같은 방식이 벡터화로 구현한 것이다.

---



- ### Neural networks learning its own features

  ##### ![content_08(7)](img/content_08(7).PNG)

  ##### hypothesis가 $g(\Theta_{10}^{2}a_{0}^{2} + \Theta_{11}^{2}a_{1}^{2} + \Theta_{12}^{2}a_{2}^{2} + \Theta_{13}^{2}a_{3}^{2})$과 같이 나오므로 위의 그림은 logistic regression과 비슷하다. 다른 점은, 입력이 feature vector 아니라, hidden layer에 의해 계산된 값의 features들이라는 것이다.

  ##### 그 features들은 $a_1^{2}, a_2^{2}, a_3^{2}$인데 이 값들은 계산되고 학습된 것이다. original features들이 아니다.

  ##### 예를 들면, layer 1에서 layer 2로 mapping하는 것은 다른 parameter 행렬 $\Theta^1$에 의해 결정된다. 따라서 neural network에서는 original input features($x_1, x_2, x_3$)를 logistic regression에 제공하지 않고 스스로 학습된 features($a_1^{2}, a_2^{2}, a_3^{2}$)들을 logistic regression에 제공한다.

  ##### ![content_08(8)](img/content_08(8).PNG)

  ##### 위와 같이 layer마다 node들이 많을 수도 있고 적을 수도 있다.

  ##### 더 많은 layer도 가능하다.

---



- ### Neural network example - computing a complex, nonlinear function of the input

  - #### Neural Network example 1: And function

    ##### ![content_08(9)](img/content_08(9).PNG)

    ##### ![content_08(10)](img/content_08(10).PNG)

    ##### 이렇게 하면 And 함수를 계산할 수 있다.

  - #### Neural Network example 2: Not function

    ##### not function은 아래와 같이 구현한다.

    ##### ![content_08(11)](img/content_08(11).PNG)

    ##### negative를 원하는 variable 앞에 큰 음수의 가중치를 둠으로써 negation function를 구현할 수 있다.

  - #### Neural Network example 3: XNOR function

    ##### XNOR function은 AND, OR, Neither를 결합함으로써 만들 수 있다.

    ##### ![content_08(12)](img/content_08(12).PNG)

---



- ### Multiclass classification

  ##### 손으로 쓴 digital 인식 문제(categories : 0 - 9)는 어떻게 해야 할까?

  ##### one vs. all classification의 확장을 사용하면 된다.

  ##### 예를 들어, pedestrian, car, motorbike, truck을 인식해야 된다면, neural network를 4개의 output unit이 있는 것으로 구현한다. 그러면 그 neural network는 4개의 숫자로 된 벡터를 출력한다.

  ##### 만약 이미지가 pedestrian이라면, 그에 상응하는 y는 [1, 0, 0, 0]으로 이루어진 벡터이다.

  ##### ![content_08(13)](img/content_08(13).PNG)

  ##### 이전에 logistic regression multiclass classification에서 y의 값을 1, 2 ,3 4로 나타냈다면, 이제는 아래와 같이 나타낸다.

  ##### ![content_08(14)](img/content_08(14).PNG)

  
