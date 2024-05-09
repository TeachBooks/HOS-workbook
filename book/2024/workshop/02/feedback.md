# Feedback, Workshop 02, EVA

## General Comments

_This section is provided to all groups._

_The solution is available in the main repository [github.com/CIE42X0-PD-24/WS02](https://github.com/CIE42X0-PD-24/WS02) and posted to the [Workbook](https://teachbooks.github.io/HOS-workbook/2024/workshop/02.html)._

Overall everyone did quite well; about half of the groups received a 9 because it was clear you understood the method well and gave thoughtful answers. The use of figures, or explicit inclusion of quantitative values in the answers made it very clear how you came to a conclusion. The other half received a 7 or lower due to: misunderstanding of the EVA methods and/or interpretation; missing answers; vague, incomplete or unclear responses, perhaps without quantitative or visual evidence. Remember the grading policy is [here](https://tudelft-citg.github.io/HOS-prob-design-24/info/#grading).

Specific comments on each question:
1. Generally well done.
2. Many of you did not get the full reason for why the figures were included. Most identified the importance of checking that the waves are big, and from a consistent direction, but almost everyone missed the point that within those waves/direction we need to check that they are all of the same type (i.e., wind versus swell waves). If this is not the case, we would need to further subdivide the data, as the observations would not be identically distributed (since the waves come from different physical sources). This is checked with steepness (hence the inclusion of period on the plot). 
3. Make sure you recognize that POT is key for creating larger samples, and that more samples means more confidence in the distribution fit. In this application there are many years of data so the difference is not huge; however, note that the design values are different (Q4), so it would make sense to use POT due to the larger number of samples _and_ the more conservative design value for Hs
4. Some of you mentioned an upper bound, but it was not clear where this came from. I know you got it from the MUDE Project 11 solution (great!), but you generally missed stating how it is derived from the parameter values for the distributions fit to this particular data set, and the implication it may have for design...e.g., what if you needed to use a higher return period?
5. About 50% of you applied the hypothesis test to check whether the excesses from POT fit a Poisson distribution. This is great, but make sure you don't forget about the 3 new validation techniques introduced in Patricia's Week 2 lecture (and in the Workbook and WS02 solution!). SFT and MR students are advised to include these in your reports (perhaps as appendices to justify the distribution choice in your text).

Additional comments:
* Many of you use code from other sources (e.g., lecture notes, MUDE, etc). This is fine (and encouraged) but please cite where you got it from, so we don't have to spend time wondering why or how you took an approach that may be slightly different form the assignments questions. Also note that it is generally important to cite and reference sources to avoid plagiarism!
* The solution uses `pyextremes` which you are welcome to use in the future for EVA- it is very easy to use.
* For marine renewables students: let me know if you are having trouble processing your data, Patricia and Robert might be able to help you out.
* Most groups had nicely formatted reports, however there were a few bugs in the way it displayed online (this did not affect your grade). As a final step when submitting your reports, you should check how they look on GitHub; any corrections are easy to make in place using the online file editor. 

## Individual Grade and Comments

_This section is for your group only._

**Grade: **

_Possible points: 0, 5, 7 or 9. See grading policy [here](https://tudelft-citg.github.io/HOS-prob-design-24/info/#grading)._

### Comments

