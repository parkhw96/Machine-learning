## Clustering

##### 	clustering은 unlabeled data로부터 학습을 하는 것이다. (정답이 주어지지 않음.)



- ### K-menas algorithm

  ##### ![image-20210705140152230](C:\Users\winner\AppData\Roaming\Typora\typora-user-images\image-20210705140152230.png)

  ##### 위와 같이 unlabeled data가 있고, 이 데이터들을 두 개의 그룹으로 묶고 싶다면,

  ##### 우선 cluster centroids라는 두 개의 점을 임의대로 할당한다. 이 cluster centroids의 개수는 내가 몇 개의 그룹으로 묶고 싶은지에 따라 결정된다.

  ##### ![image-20210705140459338](C:\Users\winner\AppData\Roaming\Typora\typora-user-images\image-20210705140459338.png)

  ##### 위와 같이 할당했다면, 이 두개의 cluster centroid에 가까운 example(초록색 점)들을 그 cluster centroid의 색으로 결정한다.

  ##### 그런 다음 이 2개의 cluster centroid들을 각각 할당된 example 점들의 평균으로 이동한다. 

  ##### example들을 할당하고, cluster centroid들을 이동시키는 작업을 반복한다.

  ##### 이번에는 알고리즘을 보게 되면, 입력으로는 K(몇 개의 묶음으로 나눌 것인지), training set이 들어가게 된다. 그리고, K개의 cluster centroids들을 임의대로 초기화 시킨다. ($\mu_1, \mu_2, ..., \mu_k$와 같이 cluster centroid를 임의대로 초기화함.)

  ![image-20210705141846707](C:\Users\winner\AppData\Roaming\Typora\typora-user-images\image-20210705141846707.png)

  ##### 위의 $c^{(i)}$는 trainging data인 $x^{(i)}$로부터 가장 가까운 cluster centroid의 index이다. 이 index는 1부터 k까지이다. cluster centroid가 1부터 k까지 있기 때문에. 예를 들어, $x^{(2)}$가 cluster centroid 3번에 가장 가깝다면, $c{(2)}$는 3이 된다. 이것을 모든 training data에 대해서 해준다.

  ##### 그리고 cluster centroid인 $\mu_k$를 cluster centroid로 index된 point들의 평균으로 업데이트 한다.



---

- ### k means optimization objective

  ##### $\mu_{c^{(i)}}$는 trainging example $x^{i}$가 속하게 된 cluster의 cluster centroid이다. 예를 들어 $x^i$가 cluster 5로 속하게 되었다고 한다면, $c^i = 5$가 될 것이고, $\mu_{c^{(i)}}$ = $\mu_5$가 된다.

  ![image-20210705143650008](C:\Users\winner\AppData\Roaming\Typora\typora-user-images\image-20210705143650008.png)

  ##### 위의 식이 optimization objective이다. 즉, 실제 example과 그 example이 속하게 된 cluster centroid의 차를 구하는 것인데,

  ![image-20210705143944770](C:\Users\winner\AppData\Roaming\Typora\typora-user-images\image-20210705143944770.png)

  ##### 즉, 그 차를 최소화 되도록 하는 $c^{(i)}, ..., c^{(m)}$과 $\mu_1, ..., \mu_k$를 구하는 것이다.

  ##### cluster centroid의 수는 example의 수보다 적어야 한다.(K < m) 만약, K > m이 되게 된다면 문제가 생긴다. 이렇게 training example로부터 K개를 뽑게 되는데, 이 경우 문제가 생길 수 있다.(local optimum)

  ![image-20210705144533212](C:\Users\winner\AppData\Roaming\Typora\typora-user-images\image-20210705144533212.png)

  ##### 우측 위의 그림과 같이 cluster centroid가 되었을 경우에는 global optimum에 도달할 수 있지만, 우측 아래의 2개의 그림과 같이 training example로부터 이상하게 cluster centroid를 골랐을 때에는 local optimum에 도달하게 되는 문제가 생긴다.

  ##### 이를 해결하기 위해서 아래의 알고리즘과 같이 한다.

  ##### ![image-20210705144900399](C:\Users\winner\AppData\Roaming\Typora\typora-user-images\image-20210705144900399.png)

  ##### 100번 정도 실행시켜보고 나면 그 데이터들을 cluster한 100개의 방법이 나오게 되는데, 그 중 가장 잘된 것을 고른다.

 

---

- ### How do we choose the number of clusters?

  ##### 데이터를 보고 K를 고르기가 힘든 경우가 있는데, 그 경우는 데이터가 애매할 때이다.

  ##### 그 경우 Elbow method가 있다. Elbow method는 다양한 K를 두고, 그때의 cost function J를 계산한다.

  ![image-20210705145538338](C:\Users\winner\AppData\Roaming\Typora\typora-user-images\image-20210705145538338.png)

  ##### 이 때 Elbow라는 K를 고른다. 허나 이 경우에는 좋은 경우의 Elbow method이고, 좋지 않은 경우(완만하게 나오는 경우) Elbow method는 별로 도움이 되지 않는다.

  ##### 다른 경우에는 예를 들어, T-shir를 파는 경우 사이즈를 어떻게 정하느냐에 따라 K=3(S, M, L)일 수도 있고, K=5(XS, S, M, L, XL)일 수도 있다. 또한 여러가지를 고려한다면 cluster의 수를 정하는데 도움을 줄 수 있다.