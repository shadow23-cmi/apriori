                                                   DMML ASSIGNMENT
                                                  APRIORI ALGORITHM



ABOUT:


	 Created a program in python3.7 to compute frequent itemsets using apriori algorithm (both fixed minimum support and multiple minimum support approach)from the data sets docword.enron.txt ,dockword.nips.txt ,dockword.kos.txt availavle at
 
http://archive.ics.uci.edu/ml/datasets/Bag+of+Words   .
    

PARAMETERS:
   
For fixed minimum support approach,
    parameters used :
          kos:
              F=0.2,0.25,0.3,0.35,0.4,0.45,0.5,0.6,0.7 and 0.1
          nips:
              F=0.2,0.3,0.4,0.5,0.6,0.7,0.8,0.9,0.95,0.98
          enron:
                ((N.B:The program didn’t run on pc. Reason:Pivot of Data set too big(8.3 G.B) to load for our program.So, ran in Google colab))
		  F=0.8,0.7,0.6,0.5,0.4,0.3,0.2,0.15,0.1
For  multiple minimum support approach,’
   parameters used:
         kos:
             F=max of ({(Total no of occurances/total no document ) for each 
			     wordId},0.05)
             phi=0.001
		 k=2,3,4,5
                  
         nips:
             F=max of ({(Total no of occurances/total no document ) for each 
			     wordId},0.01)
             phi=0.006,0.6,0.06,0.02,0.0001
		 k=10
		
                  


PROGRAM DESCRIPTION:
                  LIBRARIES USED:
                           numpy,pandas,time

     FIXED MINIMUM SUPPORT APPROACH:
                           
                 candidate-gen function(candidate_gen(f(k-1))):
                             Takes input fk-1 returns the candidate set(ck) for computing fk
                 counting support of a set(support_count_of_sets(input_set)):
                              counts the frequency of a candidate set
                            
                 Apriori function(apriori(data_clean,min_sup,k):
                      Takes input data, fixed minimum support and k(max length of frequent item set)
                       
                               

     MULTIPLE MINIMUM SUPPORT APPROACH:
   
                  Counting support of a set(support_count_of_sets(input_set)):
                              
					counts the frequency of a candidate set
                                                          
                  calculating multiple minimum supports:
                                      
                              mis_individual():  calculates mis of every word
                                        
                  Sorting according to MIS:    
                               sort_accord_mis(data):  sorts the words according to the mis
                  ms= mis_individual() (contains all the mis)
                  m=sort_accord_mis(ms) (contains all the sorted 1-items according  to mis )
                                                                                               
                  level_2_candidate_gen(m,phi):
                                generates candidate sets of size 2
					((N.B: not required as elements of f are already sorted in desired manner))
                  MS_candidate_gen(f,phi):
                                generates candidate sets of size >2
                  MS_apriori(data_clean,k,phi):
					Takes input data,k(the max size of frequent set)and phi(gives upper bound to the difference between min and maximum support
of elements a frequentt item set)
                               Otherwise,same as apriori of fixed minimum support except for 
     “    if (  support_count_of_sets(item) /no_of_transactions)>=min_sup:
                           f.append(item)  “ 
is replaced by 
     “  if(  support_count_of_sets(item)/no_of_transactions)>=ms[min(item)-1]:                           
         
                           f.append(item)    “  
where ms[min(item)-1] stores the mis of min elemnet of Ck-1
                                                               
OUTPUT:
                 output stored at:

                           	https://drive.google.com/drive/folders/1uoJ463rpRsqNUZAcoH9r4Z-n9I8nv6fo
