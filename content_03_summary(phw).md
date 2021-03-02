## Linear algebra

---



- ### <u>Matrices - overview</u>

  ##### 정사각 괄호 사이에 쓰여진 수들의 직사각형 배열(행렬)

  ##### 대게 대문자로 쓰여지며 표현된다. ex) A, B, C, X, Y

  ##### Matrix의 크기는 [Rows x Columns]이다.

  ##### 예를 들어  $R^{[r \space x\space c]}$의 의미는 R이라는 matrix는 r개의 rows(행)과 c개의 columns(열)을 가지고 있다는 의미이다.

  ##### $A_{(i,\space j)}$는 A라는 matrix에서 i번째의 row와 j번째의 column을 동시에 만족시키는 요소(값)을 의미한다.

  ---



- ### <u>Vectors - overview</u>

  ##### 벡터는 n개의 rows와 1개의 column을 가진다.

  ##### 대게 소문자로 쓰여지며 표현된다.

  $$
  y = \begin{bmatrix}
  460 \\
  232 \\
  315 \\
  178 \\ 
  \end{bmatrix}
  $$

  ##### 위와 같은 벡터는 크기가 4인 벡터이다.

  ##### $v_i$ = 벡터의 i번째 요소

  ##### 1-indexed와 0-indexed가 있지만, machine learning에서는 0-indexed가 더 유용하게 사용된다.

---



- ### <u>Matrix manipulation</u>

  ##### - Addition

  ##### 	matrix끼리 똑같은 크기이어야 한다.

  ##### 	똑같은 위치에 있는 요소끼리 더하면 된다.

  ##### 	더해져서 나온 matrix는 더해지기 전 matrix와 크기가 같다.

  

  ##### - Multiplication by scalar

  ##### 	scalar = 실수(그냥 숫자라고 생각하면 된다.)

  ##### 	scalar와 matrix의 각 요소끼리 다 곱하면 된다.

  ##### 	original matrix와 같은 크기의 matrix가 생성된다.

  

  ##### - Division by a scalar

  ##### 	곱하는 연산과 똑같이 계산한다. 단지 나누면 된다.

  

  ##### - Combination of operands

  ##### 	먼저 곱하기 혹은 나누기 연산을 진행하고 남아있는 연산을 하면 된다. 일반적으로 수학에서 하는 연산과 같	다.

  

  ##### - Matrix by vector multiplication

  ##### 	[a x b] * [b x c] = [a x c]

  ##### 	연산하는 과정과 예는 아래와 같다.

  ##### ![content_03(1)](img/content_03(1))


  ##### 	우선 두번째 벡터의 요소들 $\begin{bmatrix}1 \\5 \\ \end{bmatrix}$과 첫번째 벡터의 row $\begin{bmatrix} 1&3 \end{bmatrix}$와 곱한다. 그리고 그 결과 값들을 다 더한다. 	이로 인해 나온 숫자는 새로 만들어지는 벡터의 첫번째 요소가 된다.

  ##### 	이 과정을 첫번째 벡터의 마지막 row까지 진행한다.

  ##### A * x = y라고 두고 A는 [m x n]의 matrix, x는 [n x 1]의 vector라고 하면 여기서 A의 n(column)과 x의 n(row)은 무조건 같아야 한다. 결과는 m크기의 벡터가 된다.

  ![image-20210225205402074](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210225205402074.png)

  ##### 위 그림처럼 4개의 values와 $h_\theta(x) = -40 + 0.25x$이라면 어떻게 해야 할까?

  ##### 우선 hypothesis의 parameter들을 vector로 표현한다. $\begin{bmatrix}-40 \\ 0.25\\ \end{bmatrix}$

  ##### 이 [2 x 1]의 vector와 곱할 수 있게끔 Data Matrix를 만드는데 1들을 1번째 column에 삽입하고 2번째 column에 data(value or house sizes)를 삽입한다. 이로써 matrix가 생성된다.

  ##### 1을 삽입하는 이유는 $\theta_0$이 계산되고 표현되기 위해서 삽입한다.

  ##### 따라서 Prediction = Data Matrix * Parameters라고 표현할 수 있다.

---



- ### <u>Matrix-matrix multiplication</u>

  ##### 두번째 matrix의 각 column과 첫번째 matrix 전체를 곱하면 각각의 vector가 생성된다.

  ##### 마지막으로 각 생성된 vector를 합한다.(더한다는 의미x, 이어 붙인다는 의미)

  ##### A x B = C

  ##### 	A = [m x n]

  ##### 	B = [n x o] 

  ##### 	C = [m x o] (B가 벡터라면 o = 1이다.)

  ##### A의 column과 B의 row가 같을 때만 곱할 수 있다.

  ##### C-matrix i번째 column은 A-matrix와 B-matrix의 i번째 column의 곱 연산의 결과이다.

  ![image-20210225210709209](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210225210709209.png)

  ![image-20210225210722673](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210225210722673.png)

  ##### 위의 그림과 같이 분리해서 생각한다. 결과적으로 저 2개의 행렬을 곱하면 $\begin{bmatrix}11&10 \\ 9&14 \\ \end{bmatrix}$와 같은 matrix가 생성된다.

---



- ### <u>Implementation/use</u>

  ##### ![image-20210225210937940](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210225210937940.png)

  ##### 위의 그림과 같이 House prices에서 3개의 hypothesis와 똑같은 data set을 가지고 있다고 하자.

  ##### 이 3개의 hypothesis를 data set에 적용시키기 위해서 효과적으로 matrix-matrix multiplication을 사용할 수 있다.

  ##### 위에서 설명한 것과 같이 여기에도 적용시켜보면 우선 parameter들을 vector가 아닌 matrix로 만든다.(3개의 hypothesis가 있기 때문에)

  ##### 그렇게 되면 $\begin{bmatrix}-40&200&-150 \\ 0.25&0.1&0.4 \\ \end{bmatrix}$와 같은 matrix가 생성된다.

  ##### 그 후에 $\theta_0$를 표현하고 계산해주기 위해서 1번째 column에 1들을 삽입하고 2번째 column에는 data(house sizes)를 삽입한다.

  ##### 그렇게 되면 $\begin{bmatrix}1&2104 \\ 1&1416 \\ 1&1534 \\ 1&852 \\ \end{bmatrix}$와 같은 matrix가 생성된다.

  ##### 둘의 inner dimension이 2로 같기 때문에 곱할 수 있다.

  ##### 그 결과 $\begin{bmatrix}486&410&692 \\ 314&342&416 \\ 344&353&464 \\ 173&285&191 \\ \end{bmatrix}$와 같은 matrix가 만들어 진다.

  ##### 위의 matrix-matrix multiplication에서 보다시피 matrix와 vector간의 연산으로 보면 쉽다.

  ##### 우선 $\begin{bmatrix}1&2104 \\ 1&1416 \\ 1&1534 \\ 1&852 \\ \end{bmatrix}$와 $\begin{bmatrix}-40 \\ 0.25 \end{bmatrix}$을 곱하면 $\begin{bmatrix}486 \\ 314 \\ 344 \\ 173 \end{bmatrix}$이 나오는데, 이 때의 $\begin{bmatrix}-40 \\ 0.25 \end{bmatrix}$가 1번째 hypothesis에 대한 것이기 때문에 $\begin{bmatrix}486 \\ 314 \\ 344 \\ 173 \end{bmatrix}$는 1번째 hypothesis에 대한 예측 값이다.

  ##### 그 뒤로도 연산을 하면 2번째 hypothesis에 대한 예측 값, 3번째 hypothesis에 대한 예측 값을 각각 얻어 낼 수 있다.

  ##### 이렇게 한번에 빠르게 예측 값들을 만들어 낼 수 있다.

---



- ### <u>Matrix multiplication properties</u>

  ##### - Commutativity

  ##### 	Raw numbers / scalars 곱연산은 commutative이다. (교환법칙 성립o)

  ##### 	하지만 Matrix multiplication은 교환법칙이 성립하지 않는다.

  ##### 	A x B != B x A

  

  ##### - Associativity

  ##### 	Matrix multiplication은 결합법칙이 성립한다.

  ##### 	A x (B x C) == (A x B) x C

  

  ##### - Identity matrix(항등 행렬)

  ##### 	matrix에서는 I라고 쓴다.

  ##### 	대각선의 성분은 다 1이고 나머지는 0으로 채워진다.

  ##### 	1 x 1의 identity matrix는 1이다.

  ##### 	일반적인 A-matrix와 identity matrix를 곱하면 기존의 A-matrix가 나온다.

  ##### 	또한, AB != BA이지만, B가 identity matrix이라면 AB == BA가 성립하게 된다.

---



- ### <u>Inverse and transpose operations</u>

  ##### - Matrix inverse(역행렬)

  ##### 	숫자 중에선 0빼고 나머지 숫자들은 inverse가 존재한다. ex) $3 * 3^{-1} = 1$(여기서 1은 identity element	이다.)

  ##### 	만일 A가 [m x m]의 matrix이라면 A의 inverse는 $A^{-1}$이다. 그래서 $A * A^{-1} = I$가 된다.

  ##### 	indentity element(matrix)를 얻기 위해서 숫자든, 행렬을 곱해줘야 한다.

  ##### 	Square matrix만 inverse를 가진다.

  ​	![image-20210225213553717](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210225213553717.png)

  ##### 	어떤 matrix의 모든 요소가 0이라면 그 matrix의 inverse matrix는 없다.

  

  ##### - Matrix transpose

  ##### 	[n x m]의 matrix가 있고 이 matrix 안에 있는 값들을 유지하면서 [m x n]의 matrix로 만들려면 rows와 	columns을 swap하면 된다.

  ##### 	A-matrix([n x m])의 첫번째 row가 $A^T$의 첫번째 column이 된다.

  ##### 	위의 과정을 반복한다.

  ##### 	B-matrix가 A의 transpose이라면 B-matrix는 [m x n]의 matrix이다.

  ##### 	$A_(i,\space j) = B_(j, \space i)$

  ​	![image-20210225213922858](C:\Users\korea\AppData\Roaming\Typora\typora-user-images\image-20210225213922858.png)

