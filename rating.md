# applegoogle
#Finding number of defaulted users and spread of rating

#Understanding defaulted users.
#Install "XLConnect" package to read .xlsx file into R.
install.packages("XLConnect", repos="http...")

#Open XLConnect to use its functions.
library(XLConnect)

#Use readWorksheetFromFile() to read .xlsx file with certain sheet into R.
df <- readWorksheetFromFile("C:\\Users\\P1318124\\Desktop\\Apple & Google\\Apple and Google charge limit exceed.xlsx.xlsx",sheet=1)

#Identify defaulted users and assign it to df_default.
df_default <- df$DEFAULT_INDICATOR=="Yes"
#Expression above returns vector of boolean values and NA.

#Select non-NA values in df_default.
df_default <- subset(df_default, df_default!="NA")

#Convert df_default to numeric type to use sum().
#Expression below results in TRUE becoming 1, FALSE becoming 0.
#This is to count number of defaulted users.
sum(as.numeric(df_default))

#Identify non-defaulted users and assign it to df_default_0.
df_default_0 <- df$DEFAULT_INDICATOR=="No"

#Select non-NA values in df_default_0.
df_default_0 <- subset(df_default_0, df_default_0!="NA")

#Convert df_default_0 to numeric type to use sum().
#Expression below results in TRUE becoming 1, FALSE becoming 0.
sum(as.numeric(df_default_0))

#Select defaulted users in df.
df_default_mean <- subset(df, df$DEFAULT_INDICATOR=="Yes")

#Compute mean of past due amounts in dollars, based on the number of defaulted users.
mean(df_default_mean$PAST_DUE_AMT)

#######################################################################################################################################

#Find counts of each rating in file.

#Install the package "XLConnect" to help R read .xlsx files.
install.packages("XLConnect", repos="http...")

#Open the XLConnect library.
library(XLConnect)

#Use readWorksheetFromFile() to read a certain tab in the .xlsx file.
#Remember to use type the file's extension into the filename as input for readWorksheetFromFile.
df <- readWorksheetFromFile("C:\\Users\\P1318124\\Desktop\\Apple & Google\\Apple and Google charge limit exceed_Extract.xlsx.xlsx",sheet=2)

#Initialise a vector of length 11.
cr_vec <- rep(0, 11)

#Use for loop to iterate through each row in df, using the column MSISDN as a base.
for(i in 1:length(df$MSISDN)) {

#Use for loop to iterate through each rating (0 to 10).
for(j in 0:10) {

#Select non-NA values in the _Rating column of df.
if(!is.na(df[i,4])){

#Select cell if equals to j, i.e. rating.
if(df[i,4] == j){

#Add 1 to j to get j2, to be used as index for cr_vec.
j2 <- j+1

#Increase the count of a credit rating by 1, j, in cr_vec, using j2 as index.
cr_vec[j2] <- cr_vec[j2] + 1

}

}
}
}

#Print cr_vec to identify the total counts for each credit rating.
cr_vec

########################################################################################################################################
