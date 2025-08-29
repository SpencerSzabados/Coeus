Histograms partition a given set of observations $x_1,x_2,\dots,x_N$ into distinct bins of width $\Delta_i$ and count the number $m_i$ of observations that fall into bin $i$. These values are then normalized into probabilities (frequencies) by dividing each by the total number $N$ of observations and the associated bin width $\Delta_i$; giving $p_i = \frac{m_i}{N\Delta_i}$ for all $i=1,2,\dots, N$. 

# Density estimation
[[@Bishop_2006]]
The frequencies of a histograms bins gives a model for the density $P(X)$  that is constant over the width of each bin. 
![[Pasted image 20220608203006.png]]

Once a histogram has been computed it is no longer reliant on the original data, so when modeling large data sets, the original data no longer needs to be accessed afterwards. 

However, this modeling approach suffers in that it has jump discontinuities between bins which will not reflect the continuous nature of many underlying distributions that generated the data. Histogram modeling also suffer from high dimensionality, if each variable requires $M$ bins then for a $d$ dimensional variable there will be $M^d$ bins. 