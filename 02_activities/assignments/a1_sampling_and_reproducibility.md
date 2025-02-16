# ASSIGNMENT: Sampling and Reproducibility in Python

Read the blog post [Contact tracing can give a biased sample of COVID-19 cases](https://andrewwhitby.com/2020/11/24/contact-tracing-biased/) by Andrew Whitby to understand the context and motivation behind the simulation model we will be examining.

Examine the code in `whitby_covid_tracing.py`. Identify all stages at which sampling is occurring in the model. Describe in words the sampling procedure, referencing the functions used,sample size, sampling frame, any underlying distributions involved, and how these relate to the procedure outlined in the blog post.

Run the Python script file called whitby_covid_tracing.py as is and compare the results to the graphs in the original blog post. Does this code appear to reproduce the graphs from the original blog post?

Modify the number of repetitions in the simulation to 100 (from the original 1000). Run the script multiple times and observe the outputted graphs. Comment on the reproducibility of the results.

Alter the code so that it is reproducible. Describe the changes you made to the code and how they affected the reproducibility of the script file. The output does not need to match Whitby’s original blogpost/graphs, it just needs to produce the same output when run multiple times

# Author: YOUR NAME

Olga Demenina
Please write your explanation here...


<<Examine the code in `whitby_covid_tracing.py`. Identify all stages at which sampling is occurring in the model. Describe in words the sampling procedure, referencing the functions used, sample size, sampling frame, any underlying distributions involved, and how these relate to the procedure outlined in the blog post.>>


The provided code in ‘whitby_covid_tracing.py’ and likely, it simulates the infection and contact tracing process. It primary examined the data reported through the duration of pandemic in Jan-Dec 2020 and simulates the infection and tracing process for  individuals attending weddings(2) and brunches(80).

To identify all stages at which sampling occurring in the model, next sampling staged identified:
1.Initial Infection Sampling -  this is  form of Simple Random Sampling(SRS):
- procedure: each person at an event has a 10% chance of getting infected.
- function: within a function that assigns infections to attendees.
- sample size: 10% of the total event attendees.
- sampling frame: all individuals attending the events(weddings and brunches).
- distribution: independent probability distribution (each person has an independent chance of being infected).

2.Primary Contact Tracing Sampling -  this is also represents Simple Random Sampling(SRS):
- procedure: infected individuals have a 20% chance of being traced to an event. 
- function: within a function that determines which infected cases are successfully traced.
- sample size: 20% of infected individuals.
- sampling frame: all infected individuals.
- distribution: independent distribution (each traced individual has an independent probability of being identified).

3.Secondary Contact Tracing Sampling - this can be seen as Conditional or Threshold-based sampling:
- procedure: If two or more infections are traced to the same event, all attendees of that event are tested, leading to 100% identification of infections at that event.
- function: likely, within a function that performs comprehensive testing for events with multiple traced cases.
- sample size: all attendees of events with multiple traced infections.
- sampling frame: events where primary contact tracing has identified multiple infections.
- distribution: predetermined process once the threshold of multiple traced infections is met.


<<Run the Python script file called whitby_covid_tracing.py as is and compare the results to the graphs in the original blog post. Does this code appear to reproduce the graphs from the original blog post?>>
The script 'whitby_covid_tracing.py' run for the simulation  model with range of 1000 initially and executed successfully. 
The code aligns well with the process described in the blog.
Number of attendees are 200 for the weddings and 800 for the branches,
Infection rate at event has 10% chance of being infected(attack_rate).
Infected persons have 20% chance of being traced(trace_success).
If two or more infected persons are traced at the same event, all people at the event are tested.


 Key points of potential bias introduced by the contact tracing process include:
- The ease of identifying infections at events with organized attendee lists (e.g., weddings).
- The overestimation of infections from such events due to secondary contact tracing.


By the reason that the reproducibility is not set up yet, running the script multiple times produced the output graphs with different results and vary significantly, indicating the luck of reproducibility(random.(seed)).
I downloaded the graphs images from blog post, named 'Proportion of infections resulting from image_source'.
As followed from text it run the range of 50000 and we don't know if reproducibility is setup:
- the blue bars represent the true proportion of infections resulting from weddings. The distribution of these bars is more concentrated, primarily around the 0.2. This indicates that, in reality, about 20% of the infections are consistently attributed to weddings
- the red bars represent the proportion of cases traced to weddings through contact tracing efforts. The distribution of these bars is more spread out, ranging from 0.0 to 0.8. This broader range suggests that contact tracing often identifies a wider range of infections associated with weddings, which might not accurately reflect the true infection rate.
- the intersections between the red and blue bars shows where the observed and true proportions of infections overlap. However, these intersections are minimal, indicating that the observed data often does not match the true infection rates.
In summary the image highlights a trend regarding contact tracing at weddings as significant sources of infection.  The mean for the traced at 0.5 rate. It demonstrates that the spread of traced cases (red bars) compared to the infected cases(blue bars)  is unproportionally correlated and suggests that the observed data may have biases.


If we will compare the script's output graphs  from `whitby_covid_tracing.py` with histogram from original blog post (I run it 5 times but assigned  just 3 images as  although they are vary a bit, the concept represented is similar) we will notice that:
- the red bar(traced to the Wedding) have higher frequency and larger proportions compared to the blue bars (Infection from weddings). This indicates that a larger proportion of cases have been traced back to weddings compared to the actual infections identified from weddings. The mean (average) and median (middle value) of these red bars are likely higher, as they have higher frequencies.
- the blue bars (infections from weddings) tend to be shorter, indicating a lower reported infection rate from weddings compared to the red bar(traced to the Wedding) and centered around 20% with some variation. It's matching with histogram from original blog post.
- there is a separate red bar(traced to the Wedding) between 0.0-0.05 cases that has no intersection with blue bars. I assume it might be pointed to unreported cases from weddings or secondary transmitions related to the weddings.
- intersection of read and blue bars indicates that infections from weddings are traced back to those events.
- proportion of intersection of read and blue bars from original blog post significantly smaller then the proportion shown with histogram from original blog postt . It might be pointed that number of infected and traces cases in smaller range (1000 vs 50000) has better ratio and less biases.

[alt text](<Proportion of infections resulting from image_source.png>)
![alt text](<Proportion of infections resulting from image_run_1000_3_no producibility.png>) 
![alt text](<Proportion of infections resulting from image_run_1000_2_no producibility.png>) 
![alt text](<Proportion of infections resulting from image_run_1000_1_no producibility.png>) !


<<Modify the number of repetitions in the simulation to 100 (from the original 1000). Run the script multiple times and observe the outputted graphs. Comment on the reproducibility of the results.>>
When we run the script changing the range from 1000 to 100 times without setting the reproducibility, the script run faster but produced the stable graphs results
- the blue bars (infections from weddings) demonstrates the highest frequency around 0.2, suggestion that weddings is the consistent source of infected attendees.
- the red bar(traced to the Wedding) demonstrates the highest frequency also round 0.2, suggestion that weddings infected attendees has traced with approximately the same frequency.
- there is also a separate red bar(traced to the Wedding) between 0.0-0.05 cases that has no intersection with blue bars. Again, I assume it might be pointed to unreported cases from weddings or secondary transmitted cases related to the weddings.
- we could see that the mean for red bar(traced to the Wedding)  and blue bars (infections from weddings) specified at the point of 0.2 and closer matching  with infection registered from wedding has a higher frequency indicating that some of the cases are not traced.
In summary this repots demonstrated a better correlation between infections and tracing efforts.

![alt text](<Proportion of infections resulting from image_run_100_3_no producibility.png>) 
![alt text](<Proportion of infections resulting from image_run_100_2_no producibility.png>) 
![alt text](<Proportion of infections resulting from image_run_100_1_no producibility.png>) 


<<Alter the code so that it is reproducible. Describe the changes you made to the code and how they affected the reproducibility of the script file. The output does not need to match Whitby’s original blogpost/graphs, it just needs to produce the same output when run multiple times>>
Script updated with reproducibility with setting np.random.seed(42) in line 37
ensures that the random number generation process is consistent every time the script is run.
This means that the sequence of random numbers will be the same, resulting in the same subset of infected individuals and monitored cases each time. 
- the blue bars (infections from weddings) demonstrates the highest frequency around 0.2, suggestion that weddings is the consistent source of infected attendees.
- the red bar(traced to the Wedding) demonstrates the highest frequency also around 0.2, suggestion that weddings infected attendees has traced with approximately the same frequency.
- there is also a separate red bar(traced to the Wedding) between 0.0-0.06 cases that has no intersection with blue bars. again, I assume it might be pointed to unreported cases from weddings or secondary transmitted cases related to the weddings.
- we could see that the mean for red bar(traced to the Wedding)  and blue bars (infections from weddings) specified at the point of 0.2 and closer matching for both features.
- the graph demonstrated that after frequency mark 0.2 the blue and red bars almost matching that means the good traceability for the all infected cases.
- both red and blue bars are high and overlap, it indicates a better and more traceble correlation between infections and tracing efforts.

Running scrips multiple times, with changing the range from 1000 to 1000, run it also with a fixed seed, the compare results across multiple runs and with different versions of the code makes better undertanding of specified features. This helps in identifying the effects of changes in the code or parameters, without the interference of random variability.

![alt text](<Proportion of infections resulting from image_run_100_with_producibility.png>) 
![alt text](<Proportion of infections resulting from image_run_1000_with_producibility.png>)

In summary, reducing the number of repetitions to 100 allows for more efficient and faster testing, while setting the random seed ensures that results are reproducible and consistent, providing a solid foundation for analysis and comparison.


## Criteria

|Criteria|Complete|Incomplete|
|--------|----|----|
|Altercation of the code|The code changes made, made it reproducible.|The code is still not reproducible.|
|Description of changes|The author explained the reasonings for the changes made well.|The author did not explain the reasonings for the changes made well.|

## Submission Information

🚨 **Please review our [Assignment Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md)** 🚨 for detailed instructions on how to format, branch, and submit your work. Following these guidelines is crucial for your submissions to be evaluated correctly.

### Submission Parameters:
* Submission Due Date: `23:59 - 16/02/2025`
* The branch name for your repo should be: `assignment-1`
* What to submit for this assignment:
    * This markdown file (a1_sampling_and_reproducibility.md) should be populated.
    * The `whitby_covid_tracing.py` should be changed.
* What the pull request link should look like for this assignment: `https://github.com/<your_github_username>/sampling/pull/<pr_id>`
    * Open a private window in your browser. Copy and paste the link to your pull request into the address bar. Make sure you can see your pull request properly. This helps the technical facilitator and learning support staff review your submission easily.

Checklist:
- [x] Create a branch called `assignment-1`.
- [x] Ensure that the repository is public.
- [x] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#guidelines-for-pull-request-descriptions) and adhere to them.
- [x] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via the help channel in Slack. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.
