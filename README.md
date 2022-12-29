# disease.
#冠心病患者运动康复意愿及影响因素分析
 About learnR
 Let's learn R step by step, it is easy!

#Requirements
 R
 Rstudio
#Data
冠心病患者运动康复依从性及影响因素调查问卷 contributed by Fan Yang, thanks~

#Homework 1 (20221123)
#Target
1.Read that data
2.Measure the proprotion of second column (i.e., sex)
3.Measure the mean and sd of last column (i.e., score)

#Reference answer
Read that data:
library(readxl)
disease= read_excel("c:/Users/Lenovo/Desktop/disease.xlsx")
df = read_excel("c:/Users/Lenovo/Desktop/disease.xlsx")

#Measure the proprotion of second column (i.e., sex):
mytable=with(disease,table(df[,2])
mytable
 You will see:

女 男 
65 50 
prop.table(mytable)
       女        男 
0.5652174 0.4347826 
prop.table(mytable)*100
      女        男 
43.47826  56.52174

#Measure the mean and sd of last column (i.e., score):
vars=c(df[,67])
install.packages(pastecs)
library(pastecs)
stat.desc(vars)
You will see:
    nbr.val     nbr.null       nbr.na          min          max        range          sum       median         mean 
1.150000e+02 0.000000e+00 0.000000e+00 1.390000e+02 2.210000e+02 8.200000e+01 2.013700e+04 1.750000e+02 1.751043e+02 
     SE.mean CI.mean.0.95          var      std.dev     coef.var 
1.633618e+00 3.236184e+00 3.069013e+02 1.751860e+01 1.000466e-01 

#Homework 2 (20221128)
#Target
1.Test if the score in male and female is different.
2.Test if the education level (4th col) in male and female is different.
3.Use for loop to measure the distribution of variable in 2-10 column (i.e., sex to drink or not), one by one.

#Reference answer
#Test if the score in male and female is different.
 t.test(df[,67]~df[,2],data=disease)
 you will see:
 Welch Two Sample t-test
 data:  df[, 67] by df[, 2]
 t = -1.1689, df = 112.99, p-value = 0.2449
 alternative hypothesis: true difference in means between group 男 and group 女 is not equal to 0
 95 percent confidence interval:
  -10.033143   2.586989
 sample estimates:
 mean in group 男 mean in group 女 
        173.0000         176.7231 

#Test if the education level (4th col) in male and female is different.
  mytable<-xtabs(~df[,2]+df[,4],data=disease)
  chisq.test(mytable)
  you will see:
  Pearson's Chi-squared test

  data:  mytable
 X-squared = 3.2186, df = 4, p-value = 0.5219

 Warning message:
 In chisq.test(mytable) : Chi-squared近似算法有可能不准

 #Use for loop to measure the distribution of variable in 2-10 column (i.e., sex to drink or not), one by one. 
  for (i in names(df)[2:10]){
    print(table(df[,i]))
}
   女 男 
   65 50 
   ＜50   ≧80 50-59 60-79 
    48     3    38    26 
   其他       初中       大学       小学 高中及中专 
    2         39         16         23         35 
   ...
#Homework 3 (20221223)
#Target
 1.Measure the association between score (67th col), and sex (2nd col) to "53、当一个人心脏有问题时，他/她应该避免进行体力活动/锻炼"(66th col), one by one, with regression.For example, in your first regression, your y is score, your x is sex. In your second regression, your y is score, your x is age...
 2.Measure the association between "12、是否接受冠心病相关的健康教育" (13th col), and sex (2nd col) to "53、当一个人心脏有问题时，他/她应该避免进行体力活动/锻炼"(66th col), one by one, with regression. Note that you should use logistic regression for binary outcome.
 3.Go through this paper

#Reference answer
#Measure the association between score (67th col), and sex (2nd col) to "53、当一个人心脏有问题时，他/她应该避免进行体力活动/锻炼"(66th col), one by one, with regression.
 for (i in df[,2:66]) {print(summary(lm(df[,67]~i,data = disease)))
 }
