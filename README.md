# apriori
﻿DMML ASSIGNMENT:


MDS201935:SUMAN POLLEY
MDS201926  :ROHIT AICH BHOWMIK
 
ABOUT:


We created a program in python3.7 to compute frequent itemsets using apriori algorithm (both fixed minimum support and multiple minimum support approach)from the data sets docword.enron.txt ,dockword.nips.txt ,dockword.kos.txt availavle at 
http://archive.ics.uci.edu/ml/datasets/Bag+of+Words .
    

PARAMETERS:
   
For fixed minimum support approach,
    parameters used :
          kos:
              F=0.2,0.25,0.3,0.35,0.4,0.45,0.5,0.6,0.7 and 0.1
           nips:
              F=0.2,0.3,0.4,0.5,0.6,0.7,0.8,0.9,0.95,0.98
           enron:
                ((The program didn’t run. Reason: Data set too big to load for our program.))
For  multiple minimum support approach,’
   parameters used:
         kos:
             F=(Total no of occurances/total no document ) for each wordId
             phi=0.05,0.1,0.2
                  ((N.B: The Program didn’t terminate))
         nips:
               F=(Total no of occurances/total no document ) for each wordId
             phi=0.05,0.1,0.2
                  ((N.B: The Program didn’t terminate))


PROGRAM DESCRIPTION:
                  LIBRARIES USED:
                           numpy,pandas,time

     FIXED MINIMUM SUPPORT APPROACH:
                       Imported libraries by,
                                 import pandas as pd
                                 import numpy as np
                                 import time
                       loaded the data in pandas dataFrame by,
                             data =pd.read_csv("docword_nips.txt",skiprows=3,header=None,sep= " ",names=["docId","wordId","count"])
                             
   data_clean=data.groupby(["docId","wordId"])["count"].sum().unstack().reset_index().fillna(0).set_index("docId”)
                       Tranaction set,
                   #set of all transactions
                   Transactions=[]
                   for id in data_clean.index:
                      ls=np.flatnonzero(data_clean.loc[id]).tolist()
                      ls1=[item+1 for item in ls]
                      ls2=set(ls1)
                      Transactions.append(ls2)
                 candidate-gen function:
                      def   candidate_gen(f(k-1)):
                            It takes 2 sets from f(k-1)  : {i1,i2,,...ik-1} and {i1,i2,,...ik-1’} and  ik-1 < ik-1’ 
                                                                       do
                                                                        c={i1,i2,,...,ik-1’, ik-1’}
                                                                        C=C.append(c)
                                                                       if for all (k-1)subset s of c:
                                                                         s not in fk-1:
                                                                           C.remove(c)
                                                                        return C
                      Counting support of a set:
                              #counts the frequency of a candidate set
                             def support_count_of_sets(input_set):
                               count=0
                               for t in Transactions:
                                    if input_set.issubset(t):
                                       count =count+1
                               return count
                      Apriori function:
                          def apriori(data_clean,min_sup,k):
                               c1=[]                                                #initial pass
                               f=[]                                                   # initial pass
                               no_of_transactions=max(data_clean.index)   #  gives total no of transactions
                               start_time=time.time()
                               for item in data_clean.columns:                     # initial pass over c1
                                       c1.append(set([item]))
        
                              for item in data_clean.columns:                                                         # initial pass    

                                                                                                                                           over f1
                                   if ((data_clean[item].sum())/no_of_transactions)>=min_sup:
                                        f.append(set([item]))
                               final_f=[]
                               final_f=final_f+f
   
    
                              for i in range(2,k+1):
        
                                   c_set=candidate_gen(f)                                           #stores fk-1 to Ck 
        
                                  temp=len(f)
                                  for item in c_set:
            
                                           if (  support_count_of_sets(item) /no_of_transactions)>=min_sup:
                                                   f.append(item)                           #  now f contains k-1,k length                                
                                                                                                             frequent item sets
                             
                                                     f=f[temp:]                                       # this removes k-1 length    

                                                                                                                frequent item sets from f
                                                     final_f=final_f+f                                # appends all k length 

                                                                                                               frequent items to f_final
                                                     end_time  =time.time() 
                                                     print("F=",min_sup)
                                                     print("K=",k)
                                                     print("Runtime is :"+str(end_time-start_time)+" seconds")
                                                     print("The Frequent sets are:")
                                                     print(final_f)
                                           return final_f                                        # returns the the set ofall frequent 

                                                                                                            items
               MULTIPLE MINIMUM SUPPORT APPROACH:
                                                Imported libraries by,
                                                      import pandas as pd
                                                      import numpy as np
                                                      import time
                                               loaded the data in pandas dataFrame by,
                                                 data_clean  

                                                    =pd.read_csv("docword_nips.txt",skiprows=3,header=None,sep= "  

                                                         ",names=["docId","wordId","count"])
                                               data_clean=data.groupby(["docId","wordId"])  
                                                ["count"].sum().unstack().reset_index().fillna(0).set_index("docId”)
                       Tranaction set,
                   #set of all transactions
                   Transactions=[]
                   for id in data_clean.index:
                      ls=np.flatnonzero(data_clean.loc[id]).tolist()
                      ls1=[item+1 for item in ls]
                      ls2=set(ls1)
                      Transactions.append(ls2)
               
                      Counting support of a set:
                              #counts the frequency of a candidate set
                             def support_count_of_sets(input_set):
                               count=0
                               for t in Transactions:
                                    if input_set.issubset(t):
                                       count =count+1
                         Calculating multipke minimum supports:
                                      
                               def mis_individual():
    
                                        mis=[]
                                        no_of_transactions=max(df1.index)
                                      print(no_of_transactions)
                                      for item in data_clean.columns:
                                           mis.append((df1[item].sum())/no_of_transactions)
                                      return mis
                                 Sorting according to MIS:    
                                         def sort_accord_mis(data):
    
                                              vals=np.array(data)
                                              vals1=np.argsort(vals)
                                              vals2=[item+1 for item in vals1]
                                         return vals2


                           ms= mis_individual()                 #contains all the mis
                           m=sort_accord_mis(ms)                          #contains all the sorted 1-items according 

                                                                                                to mis 
                                def level_2_candidate_gen(m,phi):
                                     generates candidate sets of size 2
                                 def MS_candidate_gen(f,phi)::
                                     generates candidate sets of size >2
                                def MS_apriori:
                                     same as apriori of fixed minimum support except for 
                                              “    if (  support_count_of_sets(item) /no_of_transactions)>=min_sup:
                                                   f.append(item)  “ is replaced by 
                                               “  if (  support_count_of_sets(item) 

                                                              /no_of_transactions)>=ms[min(item)-1]:
         
                                                                f.append(item)    “  where ms[min(item)-1] stores the mis of min elemnet of Ck-1
                                                               
                                  def MS_apriori(data_clean,k,phi):
    
    f=[]
    start_time=time.time()
    
    for item in m:
        if ((data_clean[item].sum())/no_of_transactions)>=ms[item-1]:
            f.append(set([item]))
    final_f=[]
    final_f=final_f+f
   
    
    for i in range(2,k+1):
        if k==2:
            print("t")
            c_set=level_2_candidate_gen(m,phi)
            print(c_set)
        else:
            c_set=MS_candidate_gen(f,phi)
        temp=len(f)
        for item in c_set:
            
            if (  support_count_of_sets(item) /no_of_transactions)>=ms[min(item)-1]:
                f.append(item)                           #  now f contains k-1,k length frequent item sets
                             
        f=f[temp:]                                       # this removes k-1 length frequent item sets from f
        final_f=final_f+f                                # appends all k length frequent items to f_final
    end_time  =time.time() 
   
    print("K=",k)
    print("Runtime is :"+str(end_time-start_time)+" seconds")
    print("The Frequent sets are:")
    print(final_f)
    return final_f



                    OUTPUT:
                              output stored at:

                         https://drive.google.com/open?id=1uoJ463rpRsqNUZAcoH9r4Z-n9I8nv6fo
