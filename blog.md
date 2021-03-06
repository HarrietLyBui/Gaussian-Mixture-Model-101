<center> <h1> GAUSSIAN MIXTURE MODEL 101 </h1>  </center>

<h2><b>Define a problem</b></h2>
<strong>Problem:</strong>

<span style="font-weight: 400;">You are building a game and you want to predict if a particular player will play again next month or not. You are classifying your player as going to churn or not going to churn. This is obviously a classification problem!</span>

<b>What you are given: </b>

<span style="font-weight: 400;">What information do you have to make your prediction and solve the problem above? Just one single data point which is the amount of money that the user has spent in the game this month. The money can be withdrawn or deposited to buy some currency or power in the game. </span>

<span style="font-weight: 400;"><strong>What is unique in this situation:</strong> You only have </span><b>one </b><span style="font-weight: 400;">data point! Usually if you want to predict customers’ churn, we want to have several data points such as the time the users has logged in and many different features. However, for this example we only use one dimensional data point. </span>

<span style="font-weight: 400;"><strong>Solution:</strong> In order to solve this problem, we will apply Gaussian Mixture Model. What is it model exactly?</span>

<span style="font-weight: 400;">Gaussian Mixture Model is </span>
<ul>
	<li style="font-weight: 400;"><span style="font-weight: 400;">A generative unsupervised clustering technique.</span></li>
	<li style="font-weight: 400;"><span style="font-weight: 400;">Also known as EM clustering</span></li>
	<li style="font-weight: 400;"><span style="font-weight: 400;">Idea: each point is generated by linearly combining multiple multivariate Gaussians</span></li>
</ul>
<span style="font-weight: 400;">In order to understand that big idea I just described above, let’s break each down the magic word “Gaussian”</span>
<h2><b>What is a Simple Gaussian?</b><b>
</b><b>
</b></h2>
<span style="font-weight: 400;">A Gaussian is a distribution. A distribution contains two main group of items:</span>
<ul>
	<li style="font-weight: 400;"><span style="font-weight: 400;"> a list of all possible outcomes generated from an experiment</span></li>
	<li style="font-weight: 400;"><span style="font-weight: 400;">Probabilities associated with each outcomes </span></li>
</ul>
<span style="font-weight: 400;">An example of a distribution: We have a game and we would like to keep track of players’ score. Below is an example of one player’s score. She cores 1 four times, 2 9 times, etc. The largest number in the frequency column is 9, which is the peak.</span>

<center> <img class=" size-full wp-image-119 aligncenter" src="https://inlovewithanaspie.files.wordpress.com/2018/12/frequency-distribution-table.gif" alt="frequency distribution table" width="600" height="710" /> </center>

<span style="font-weight: 400;">If we plot our frequency table out in a graph, we will see a bell curve approximately.</span>

<center> <img class=" size-full wp-image-120 aligncenter" src="https://inlovewithanaspie.files.wordpress.com/2018/12/bell.png" alt="bell" width="450" height="327" /> </center>

<span style="font-weight: 400;">This bell curve is  a Gaussian distribution! So a Gaussian distribution is a distribution where half of the data points fall to the left of the graph and half of the data points fall to the right of the graph. It is an even distribution. A Gaussian distribution is also called a normal distribution. </span>

<b>Define a Gaussian distribution mathematically:</b>

<span style="font-weight: 400;">In order to define a Gaussian distribution, we need two variables: a mean and a standard deviation.</span>
<ul>
	<li style="font-weight: 400;"><span style="font-weight: 400;">A mean is the average of all the data points and it defines the center of the bell curve.</span></li>
	<li style="font-weight: 400;"><span style="font-weight: 400;">A standard deviation describes how spread out the data is. </span></li>
</ul>
<span style="font-weight: 400;">When you have a dataset that increases to a peak and then decreases, you can use the Gaussian distribution to model your data. For example, a car’s velocity increases to a peak and then decreases. A sound gets louder to a peak and then drifts out. Neat!</span>

<span style="font-weight: 400;">Now recall a distribution is a list of outcome and probabilities associated with those outcomes. For the problem we define at the beginning, the list of outcome is the single data point we have for each player - the money the user spends in the game this month (x) We will use mean and standard deviation from our data to calculate these probabilities. A formal name of this formula is probability density function (y).</span>

<img class=" size-full wp-image-124 aligncenter" src="https://inlovewithanaspie.files.wordpress.com/2018/12/simple-gaussian.jpg" alt="simple gaussian" width="450"  />

<span style="font-weight: 400;">When we plot out x and y, we have the bell curve graph with y is represented on the vertical axis and x is represented on the horizontal axis. Different means and standard deviation produce different bell curves with different colors below:</span>
<h2><b>What is a Multivariate Gaussian?</b></h2>
<img class=" size-full wp-image-123 aligncenter" src="https://inlovewithanaspie.files.wordpress.com/2018/12/multivariate-guassian.png" alt="multivariate guassian" width="100%" />

<span style="font-weight: 400;">Above is the equation to computer one Gaussian distribution in case of a dataset with multiple dimensions. Note that this is not the distribution of all the sub Gaussian distributions in our dataset. We create a vector x out of all data points with d dimensions (d features) in the dataset. The T next to the x vector parenthesis denotes a vector transpose. Our output of this equation will be a vector of probability density. Different from Gaussian distribution, Multivariate Gaussian does not use standard deviation but the covariance matrix. When we the dataset is high dimensional, covariance matrix gives us a more accurate result of the probability.</span>
<h2><b>Gaussian Mixture Model (GMM)</b></h2>
<span style="font-weight: 400;">Now as we understand what a Gaussian distribution is we can talk about a Gaussian Mixture Model. When the dataset has multiple distributions, meaning it has multiple peaks and we want to represent all of these distributions in one model, we can use the Gaussian Mixture Model. Therefore, it is basically a probability distribution that consists of multiple probability distributions, which are multiple Gaussians.</span>

<img class="alignnone size-full wp-image-121 aligncenter" src="https://inlovewithanaspie.files.wordpress.com/2018/12/gmm.png" alt="GMM" width="100%"  />

<span style="font-weight: 400;">K is the number of distributions in the dataset (the number of peaks). In the case where d=1 above we see three peaks => K = 3. In order to compute the overall distribution: </span>
<ul>
	<li style="font-weight: 400;"><span style="font-weight: 400;">Compute the Gaussian distribution (N) K times for each sub distribution following the Gaussian distribution formula for d dimensions.. Although we have K different distributions in the dataset, we only have one big vector x. </span></li>
	<li style="font-weight: 400;"><span style="font-weight: 400;">Multiply the result of Gaussian distribution for each sub distribution with the prior probability (weight). This weight can be interpreted as size of the sub distribution. Each bell curve has different height. </span></li>
	<li style="font-weight: 400;"><span style="font-weight: 400;">Compute the sum of all the multiplications generated from the above step. </span></li>
</ul>
<span style="font-weight: 400;">After doing this computation, we generate a continuous bell curve for our data points instead of having multiple separated bell curves for each distribution. Using this continuous bell curves, we can solve classification problems by clustering.</span>
<h2><b>Machine Learning Application for GMM: Unsupervised Clustering</b></h2>



<span style="font-weight: 400;">Coming back to our example at the beginning. Our data is the money users spend this month in the game. We want to classify them into two groups: to churn or not to churn (will play again next month or not). So naturally we would assume that there are two distributions in the dataset. Therefore our dataset can be represented with Gaussian Mixture Model. Given the amount of money one user spends, which is our datapoint x, we can estimate the prior probability (weight) of this data point for each of the sub distribution. On the other word, estimate the probability of that player belonging to the group playing next month (w1) or the group not playing next month (w2). The player will be assigned to the group with higher weight (higher probability or higher size). If w1 > w2, the player will play next month. If w1<w2, the player will not play next month. If w1 = w2 we are not sure whether the player will play next month or not. 

<br>The big question here is how do we estimate the parameters of GMM? We will go through a process called Expectation Maximization to estimate the parameters of GMM. In statistics, the fancy name for the process of estimating parameters of a model is called maximum likelihood estimation. Given the observations we try to maximize the log likelihood function. <br>
</span>

<span style="font-weight: 400;">Why do we use GMM over Kmeans?</span>
<ul>
	<li style="font-weight: 400;"><span style="font-weight: 400;">Clusters are overlapped in the feature space. Kmeans will not be able to tell one group from the other because it only assigns each data point to exactly one cluster. </span></li>
	<li style="font-weight: 400;"><span style="font-weight: 400;">Clusters are defined by non-circular shape. Kmeans only uses Euclidean distance.</span></li>
</ul>
<h2><b>References </b></h2>
<span style="font-weight: 400;">[1] Ihler, Alexander. “Machine Learning and Data Mining, Clustering.” </span>

<span style="font-weight: 400;">[2] </span><span style="font-weight: 400;">Raval Siraj. </span><span style="font-weight: 400;">“Gaussian Mixture Model” </span><a href="https://github.com/llSourcell/Gaussian_Mixture_Models/blob/master/intro_to_gmm_%26_em.ipynb"><span style="font-weight: 400;">https://github.com/llSourcell/Gaussian_Mixture_Models/blob/master/intro_to_gmm_%26_em.ipynb</span></a>
<span style="font-weight: 400;">
	<br>[3] “Maximum Likelihood Estimation”. Wikipedia. </span><a href="https://en.wikipedia.org/wiki/Maximum_likelihood_estimation"><span style="font-weight: 400;">https://en.wikipedia.org/wiki/Maximum_likelihood_estimation</span></a>
