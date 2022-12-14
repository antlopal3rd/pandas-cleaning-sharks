# pandas-cleaning-sharks

Analysis on a kaggle database on global shark attacks

link original database: https://www.kaggle.com/datasets/teajay/global-shark-attacks

The database was in very poor condition with lots of missing values. In fact, in every column there were a lot of null values. Since the Case Number could be deduced from the Date column, I deleted the rows were both values were missing. 17020 rows were deleted. One row was fixed manually.

Then I deleted duplicated rows which further reduced the database in 2392 rows. 9 rows were also deleted where the date was missing and that left these two previous columns without null values.

Year and Type were the two following columns which only had two and four missing values respectively. Year values were fixed manually since are the same as case number, but Type had to be set to “Invalid”.

Investigator or Source column had only 17 values missing and were replaced by “unknown”. One value in Href Formula was missing and was replaced manually by the corresponding value of Href column which are the same.

Rows were Injury and Fatal (Y/N) data were missing were deleted leaving the dataset with 6295 rows.

Rows were Country, Area, and Location were missing at the same time were deleted since we can´t place where it happened if at all.

4 rows were left with null values in Country were two of them were fixed manually with information from other columns and two of them had to be deleted.

The Species column was particularly troublesome. There were thousand of unique values with numbers and special characters also in them. I removed these conditions with a regex function, eliminated spaces before and after with string functions and then proceeded to make dozens of filters to capture each species of shark. Were the shark species could not be determined just “shark” was written in the column. “Questionable” was written were doubts about the incident were raised and there was also 104 rows were “invalid” which were present in the original version of the database. After all the filters some rows remained with a frequency value of one. All these rows were set to “shark”

In the Injury column I followed the same path as in the previous one. Non-fatal bite injuries were separated by parts of the body and the rest of them in other categories. As in the Species column after applying all filters data with a frequency of one was set to “other”

Since the Injury column now doesn’t have null values and provides a lot of information on the next column – Fatal (Y/N)- the cleaning process was a lot easier. I compared the two columns to see if the injuries sustained were fatal or not and in the case of drowning and questionable, I decided to insert them as UNKNOWN.

## Findings:

1. 81.1% of injuries were non-fatal, 13.64% resulted on death and on 5.26% we have no information.

2. In order of most to least common injuries:

laceration
no injury          
fatal              
leg bitten         
foot bitten        
other              
minor injury       
hand bitten        
puncture wound     
arm bitten         
drowning           
questionable        
thigh bitten        
calf bitten         
ankle bitten        
survived            
shoulder bitten     
fingers bitten      
knee bitten         
torso bitten        
head bitten         
wrist bitten        
buttocks bitten

3. According to the type of attack 64.96% were unprovoked attacks, 14.53% was invalid data 11.89 were provoked attacks, 7.19% attacks during boating and 0.96% were attacks during sea disasters

4. According to the species of sharks producing these attacks in order of most to least likely they were:

shark (exact species not identified)               
white shark           
questionable          
tiger shark           
bull shark            
invalid               
blacktip shark         
bronze whaler          
nurse shark            
blue shark             
mako shark             
wobbegong shark        
hammerhead shark       
raggedtooth shark      
grey nurse shark       
lemon shark            
zambesi shark          
sand shark             
spinner shark          
sevengill shark        
dusky shark            
dogfish shark          
copper shark            
galapagos shark         
basking shark           
porbeagle shark         
angel shark             
silky shark             
gill shark              
carpet shark            
goblin shark            
salmon shark            
leopard shark           
silvertip shark       
whale shark 


