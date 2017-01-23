# Introduction {#intro}

데이터 마이닝 프로세스로는 크게 3가지 방법이 있다. 
* CRISP-DM : Business Understand- Data Understandiung- Data Preparation- Modeling- Evaluation- Deployment 
* KDD : Selection- Preprocessing- Transformation- Data Mining- Interpretation/Evaluation 
* SEMA : Sample- Explore- Modify- Model- Assess

> [추천] 각 단계별 간략한 설명은 [Dr. Saed Sayad](http://www.saedsayad.com/data_mining_map.htm) 사이트를 참고 바란다. 

CRISP-DM는 "Cross Industry Standard Process for Data Mining"의 약어로 오늘날 가장 많이 사용되는 데이터 처리 방법론중 하나이다[1]. 

본 문서에서는 [CRISP-DM](https://en.wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining)데이터 처리 순서에 따라서 내용을 작성 하였다[2]. 


## CRISP-DM
![](/assets/dm.PNG)

CRISP-DM에 따르면 가장 첫 부분에는 "Business Understaing"부터 시작하지만, 기술적인 부분이 낮아 Introduction 챕터와 함께 간략하게만 설명 한다. 





## Business Understanding

This initial phase focuses on understanding the project objectives and requirements from a business perspective, and then converting this knowledge into a data mining problem definition, and a preliminary plan designed to achieve the objectives. A decision model, especially one built using the Decision Model and Notation standard can be used.






















You can label chapter and section titles using `{#label}` after them, e.g., we can reference Chapter \@ref(intro). If you do not manually label them, there will be automatic labels anyway, e.g., Chapter \@ref(methods).

Figures and tables with captions will be placed in `figure` and `table` environments, respectively.

```{r nice-fig, fig.cap='Here is a nice figure!', out.width='80%', fig.asp=.75, fig.align='center'}
par(mar = c(4, 4, .1, .1))
plot(pressure, type = 'b', pch = 19)
```

Reference a figure by its code chunk label with the `fig:` prefix, e.g., see Figure \@ref(fig:nice-fig). Similarly, you can reference tables generated from `knitr::kable()`, e.g., see Table \@ref(tab:nice-tab).

```{r nice-tab, tidy=FALSE}
knitr::kable(
  head(iris, 20), caption = 'Here is a nice table!',
  booktabs = TRUE
)
```

You can write citations, too. For example, we are using the **bookdown** package [@R-bookdown] in this sample book, which was built on top of R Markdown and **knitr** [@xie2015].

---
[1]: http://www.kdnuggets.com/2014/10/crisp-dm-top-methodology-analytics-data-mining-data-science-projects.html "KDNuggets Poll"
[2]: ftp://public.dhe.ibm.com/software/analytics/spss/documentation/modeler/14.2/en/CRISP_DM.pdf "IBM SPSS Modeler CRISP-DM" Guide
