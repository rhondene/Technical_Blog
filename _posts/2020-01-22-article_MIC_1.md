# On Maximal Information Coefficient:  A Modern Approach for Finding Associations in Large Data sets

<em>In this two-part</em> <em>blog post, I will share with you the idea behind maximal information coefficient, MIC, and how it is applied to find a wide range of relationships in large data sets.</em>

<strong>Part 1</strong>

I recently came came across David and Yakir Reshef’s presentation on ‘<em>Detecting Novel Associations in Large Data sets’</em>  (namesake of their <a href="http://science.sciencemag.org/content/334/6062/1518">paper</a>) at the <em>2017 Broad Institute Models, Inference and Algorithms</em> meeting (<a href="https://www.youtube.com/playlist?list=PLlMMtlgw6qNjROoMNTBQjAcdx53kV50cS">video playlist</a>)  where they presented the intuition and applications of their recently developed association metric the <strong>maximal information coefficient (MIC)</strong> that is based on information theory<strong>. </strong> They gave such an enlightening and convincing presentation that the following day I read as many articles on MIC that I could find. This article provides an overview of the association metrics, a high-level explanation of MIC, its advantages and disadvantages, and programming packages to implement MIC.

<strong>Measuring Associations:</strong>

21<sup>st </sup><sub> </sub>century biological research is powered by high-throughput experiments that generate high-dimensional data with many, even thousands of, variables or features. Identifying the kind of relationships (aka <em>associations</em>) between these variables is necessary for gaining insights about our experiments or to choose the best set of features for making an accurate model since not all features may be useful. We compute <strong>measures of association </strong>to quantify the strength and/or direction (positive or negative) of relationship between two variables. Quantifying the relationship between variables infers whether they are dependent or independent. A value of zero means no statistical correlation between the variables.

There are several parametric and non-parametric measures for association, such as <em>Pearson’s R</em>, <em>distance correlation</em>, <em>mutual information</em>, etc. However, some correlation metrics are limited to the kinds of association they can detect, or they make assumptions about the underlying distributions of the variables. For example, Pearson’s R only detects linear dependencies. Thus, two variables can have a <em>Pearson’s R = 0.0 but still be dependent</em>. Given that many biological processes are defined by complex patterns that deviate from linear behaviour, we would to like to use a more versatile association statistical method. Enter the maximal information coefficient.

<img class="alignnone  wp-image-26" src="https://rhondenewint.files.wordpress.com/2018/12/types_association_variables.jpg" alt="types_association_variables" width="336" height="205" /><em>Types of relationships(R.Wint)</em>

<strong>Maximal Information Coefficient</strong>

<b>Maximal information Coefficient (</b>Reshef ,Reshef  et al 2011) is an information theory-based measure of association that can capture a wide range of functional and non-functional relationships between variables.

<figure> <img src="https://rhondenewint.files.wordpress.com/2018/12/mic_yeshef.jpg?w=450" width=" height=" />
<figcaption><i>Comparison of MIC to other measures of association (Yeshef et al 2011)</i>.</figcaption></figure>Formally, MIC is equal to the coefficient of determination (R<sup>2</sup>).  MIC takes values between 0 and 1, where 0 means statistical independence and 1 means a completely noiseless relationship.

<img class="alignnone  wp-image-27" src="https://rhondenewint.files.wordpress.com/2018/12/mic_formula.jpg" alt="MIC_formula" width="352" height="47" />

From the formula we can see that  <strong>MIC(X,Y)</strong> is the mutual information between random variables X and Y normalized by their minimum joint entropy. I interpret the MIC as the percent of a variable Y that can be explained by a variable X. In addition to generalizing well over a range of relationships, another useful property of MIC is its <em>equitability</em>. This means that MIC assigns the same score to equally noisy relationships, regardless of the type of relationship. This is good because a lot of times we do not know the distribution of our data or the nature of relationships between variables.

<strong>Pros of MIC</strong>:
<ul>
	<li>Able to capture wide range of linear and non-linear relationships (cubic, exponential, sinusoidal, superposition of functions)</li>
	<li>Symmetric because it is based on mutual information.</li>
	<li>Does not make any assumptions about the distribution of the variables.</li>
	<li>Robust to outliers because of its mutual information foundation.</li>
	<li>MIC coefficient ranges from [0,1] which makes for ease of interpretation and comparison.</li>
</ul>
<strong>Cons of MIC:</strong>
<ul>
	<li>Does not report the direction or the type of relationship.</li>
	<li>Computationally expensive. However, several optimized algorithms for approximating the MIC have been published.</li>
	<li><em>Statistical power deficiency</em>: when <a href="http://statweb.stanford.edu/~tibs/reshef/comment.pdf">Simon and Tibshirani </a>compared the performance of MIC with Pearson's and distance correlation on simulated independent data, they reported that in most cases MIC had less power.
<figure><img class="alignnone  wp-image-29" src="https://rhondenewint.files.wordpress.com/2018/12/simon_tib_mic.jpg" alt="simon_tib_MIC" width="638" height="298" /></figure></li>
</ul>
<i>Simon and Tibshirani 2011</i>

<strong>Resources for MIC in python and R</strong>

If you would like to try out MIC on your data, here is a <a href="https://pypi.org/project/mictools/">python package</a> and an <a href="https://cran.r-project.org/web/packages/minerva/minerva.pdf">R package</a>.
 
