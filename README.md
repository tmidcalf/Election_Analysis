# Election_Analysis

## Project Overview

A Colorado Board of Elections employee has asked us to complete an election audit for a recent congressional election.

## Results

- Using the code below, I found how many total votes were cast in this election and I counted up all the votes cast for each individual county.
  ```
  for row in reader:
    total_votes = total_votes + 1
    county_name = row[1]

    if county_name not in county_list:
      county_list.append(county_name)
      county_votes[county_name] = 0

    county_votes[county_name] += 1
  ```
  
  The results from this code returned 369,711 votes were cast in this election.

  ![alt text](https://github.com/tmidcalf/Election_Analysis/blob/main/Resources/total_votes.png?raw=true)

- Using the code below, I determined the percentage of the total votes cast that each county received and I determined which county had the largest turnout of voters
  ```
  for county_name in county_votes:
    county_vote_count = county_votes.get(county_name)

    county_vote_percentage = float(county_vote_count) / float(total_votes) * 100
            
    county_results = (
        f"{county_name}: {county_vote_percentage:.1f}% 
        ({county_vote_count:,})\n")
            
    if (county_vote_count > largest_county_count):
        largest_county_count = county_vote_count
        largest_county = county_name
  ```

  Running this block of code returned the following results for each county.

  ![alt text](https://github.com/tmidcalf/Election_Analysis/blob/main/Resources/county_votes.png?raw=true)
- The county with the largest turnout of voters was Denver with 306,055 votes, which was 82.8% of the votes.

  ![alt text](https://github.com/tmidcalf/Election_Analysis/blob/main/Resources/county_summary.png?raw=true)
    
- Using the code below, I determined the total votes cast for each candidate in the election. 
  ```
  for row in reader:
    candidate_name = row[2]

    if candidate_name not in candidate_options:
      candidate_options.append(candidate_name)
      candidate_votes[candidate_name] = 0

    candidate_votes[candidate_name] += 1
  ```

  Then, with this block of code found the percent of the total votes were cast for each candidate and determined a winning candidate.
  ```
  for candidate_name in candidate_votes:

    votes = candidate_votes.get(candidate_name)
    vote_percentage = float(votes) / float(total_votes) * 100
    candidate_results = (
      f"{candidate_name}: {vote_percentage:.1f}% ({votes:,})\n")

      print(candidate_results)

    if (votes > winning_count) and (vote_percentage > winning_percentage):
      winning_count = votes
      winning_candidate = candidate_name
      winning_percentage = vote_percentage
  ```

- Using this block of code I could analyze the results of the election and determine that Diana DeGette was the winner with 73.8% of the vote, or 272,892 votes. This is shown in the image below.

  ![alt text](https://github.com/tmidcalf/Election_Analysis/blob/main/Resources/candidate_results.png?raw=true)

## Resources

- Data Source: election_results.csv
- Software: Python 3.7.6, Visual Studio Code 1.66.2
  
## Summary

Because this script is more general we can use it for any set of election data with a few modifications. For example, if this were to be used for a presidential election we could add code to determine the amount of votes each candidate received from each county and then calculate what candidate won the county. From there, we could write a block of code that counts up the total counties each candidate won and whichever candidate has the most won counties in the state would win all the electoral votes for that state.
