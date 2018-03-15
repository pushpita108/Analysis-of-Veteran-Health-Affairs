ReadMe File:

In order to get the visualisation results as presented in report , please follow the steps:

1) Download the fuseki server

2) Start fuseki server using the following command 
    java -jar fuseki-server.jar --update --loc=dataDir /myDataset  

3) Open http://loccalhost:3030 in the web browser.

4) Create a new in memory dataset named 'sample'. Load data-1152.nt with destination graph name data1152 ,data-1210.nt with destination graph name data1210, data-1212.nt with destination graph name data1212 ,data-1205.nt with destination graph name data1205 , data-1537.nt with destination graph name data1537 ,data-1538.nt with destination graph name data1538 into sample dataset to the server. 

5) Execute the  SPARQL queries from Queries.txt. The output is obtained in the json format.

6) Open the following links in web browser:(These are the outputs in json format)

a) Comparison of veteran population with number of ICU and emergency beds in given time frame 
 
http://localhost:3030/sample/query?output=json&query=%0APREFIX+xsd%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2001%2FXMLSchema%23%3E%0APREFIX+voc1%3A%3Chttp%3A%2F%2Fdata-gov.tw.rpi.edu%2Fvocab%2Fp%2F1202%2F%3E%0APREFIX+voc2%3A%3Chttp%3A%2F%2Fdata-gov.tw.rpi.edu%2Fvocab%2Fp%2F1150%2F%3E%0APREFIX+g%3A%3Chttp%3A%2F%2Flocalhost%3A3030%2Fsample%2Fdata%2F%3E%0A%0ASELECT+distinct%0A(SUM(xsd%3Adecimal(%3Fpop))+AS+%3Fpopulation)+(SUM(xsd%3Adecimal(%3FnoICU))+AS+%3FICU)%0A(SUM(xsd%3Adecimal(%3FnoEB))+AS+%3FEmergencyBeds)%0A%3Fstate%0AFROM+NAMED++%3Chttp%3A%2F%2Flocalhost%3A3030%2Fsample%2Fdata%2Fdata1152%3E%0AFROM+NAMED++%3Chttp%3A%2F%2Flocalhost%3A3030%2Fsample%2Fdata%2Fdata1210%3E%0AWHERE+%7B%0AGRAPH+g%3Adata1152%0A++%7B%0A%3Fs+voc2%3Aveteran_population+%3Fpop.+%0A%3Fs+voc2%3Astate+%3Fstate.%0A++%7D%0A++GRAPH+g%3Adata1210%0A++%7B%0A%3Fs1+voc1%3Aintensive_care_unit_class+%3FnoICU.%0A%3Fs1+voc1%3Aemergency_room_beds+%3FnoEB.%0A%3Fs1+voc1%3Astate+%3Fstate.%0A++%7D%0A%7Dgroup+by+%3Fstate+order+by+%3Fstate

b) Comparison of number of veteran patients and hospital staff for each state 

http://localhost:3030/sample/query?output=json&query=PREFIX+xsd%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2001%2FXMLSchema%23%3E%0APREFIX+voc%3A%3Chttp%3A%2F%2Fdata-gov.tw.rpi.edu%2Fvocab%2Fp%2F1202%2F%3E%0APREFIX+g%3A%3Chttp%3A%2F%2Flocalhost%3A3030%2Fsample%2Fdata%2F%3E%0ASELECT+distinct%0A(SUM(xsd%3Adecimal(%3Finp))+AS+%3Finpatient)+(SUM(xsd%3Adecimal(%3Foutp))+AS+%3Foutpatient)%0A(SUM(xsd%3Adecimal(%3Fphy))+AS+%3Fphysician)+(SUM(xsd%3Adecimal(%3Fnur))+AS+%3Fnursing)+%0A(SUM(xsd%3Adecimal(%3Fprof))+AS+%3Fprofessionals)+%3Fstate%0AFROM+NAMED++%3Chttp%3A%2F%2Flocalhost%3A3030%2Fsample%2Fdata%2Fdata1205%3E%0AFROM+NAMED++%3Chttp%3A%2F%2Flocalhost%3A3030%2Fsample%2Fdata%2Fdata1212%3E%0AWHERE+%7B%0A+GRAPH+g%3Adata1212%7B+%0A%3Fs+voc%3Ainpatient+%3Finp.%0A%3Fs+voc%3Aoutpatient+%3Foutp.%0A+%3Fs+voc%3Astate+%3Fstate.%7D%0A+GRAPH+g%3Adata1205%7B+++%0A%3Fs1+voc%3Astaffing_physicians+%3Fphy.%0A%3Fs1+voc%3Astaffing_nursing+%3Fnur.%0A%3Fs1+voc%3Astaffing_other_health_professionals+%3Fprof.+%0A%3Fs1+voc%3Astate+%3Fstate.%0A+%7D%0A%7D+group+by+%3Fstate+order+by+%3Fstate

c) State-wise comparison of number of veteran inpatients to number of emergency health care facility 

http://localhost:3030/sample/query?output=json&query=PREFIX+xsd%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2001%2FXMLSchema%23%3E%0APREFIX+voc%3A%3Chttp%3A%2F%2Fdata-gov.tw.rpi.edu%2Fvocab%2Fp%2F1202%2F%3E%0APREFIX+g%3A%3Chttp%3A%2F%2Flocalhost%3A3030%2Fsample%2Fdata%2F%3E%0ASELECT+distinct%0A(sum(xsd%3Adecimal(%3Finp))+AS+%3Finpatient)+(sum(xsd%3Adecimal(%3FnoICU))+AS+%3FICU)%0A(sum(xsd%3Adecimal(%3FnoEB))+AS+%3FEmergencyBeds)%0A%3Fstate%0AFROM+NAMED++%3Chttp%3A%2F%2Flocalhost%3A3030%2Fsample%2Fdata%2Fdata1210%3E%0AFROM+NAMED++%3Chttp%3A%2F%2Flocalhost%3A3030%2Fsample%2Fdata%2Fdata1212%3E%0AWHERE+%7B%0AGRAPH+g%3Adata1212%0A+%7B%0A%3Fs+voc%3Ainpatient+%3Finp.+%0A%3Fs+voc%3Astate+%3Fstate.%0A++%7D%0A++GRAPH+g%3Adata1210%0A++%7B%0A%3Fs1+voc%3Aintensive_care_unit_class+%3FnoICU.%0A%3Fs1+voc%3Aemergency_room_beds+%3FnoEB.%0A%3Fs1+voc%3Astate+%3Fstate.%0A++%7D%0A%7D+group+by+%3Fstate++order+by+%3Fstate


d) State-wise comparison of total pension and compensation for veterans in years 2007 and 2008

http://localhost:3030/sample/query?output=json&query=PREFIX+xsd%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2001%2FXMLSchema%23%3E%0APREFIX+voc1%3A%3Chttp%3A%2F%2Fdata-gov.tw.rpi.edu%2Fvocab%2Fp%2F1538%2F%3E%0APREFIX+voc2%3A%3Chttp%3A%2F%2Fdata-gov.tw.rpi.edu%2Fvocab%2Fp%2F1537%2F%3E%0APREFIX+g%3A%3Chttp%3A%2F%2Flocalhost%3A3030%2Fsample%2Fdata%2F%3E%0ASELECT+%0A(SUM(COALESCE(xsd%3Adecimal(%3Fcomp_yr1)%2C0))+AS+%3Fcompensation_2008)+%0A(SUM(COALESCE(xsd%3Adecimal(%3Fcomp_yr2)%2C0))+AS+%3Fcompensation_2007)+%0A%3Fstate%0AFROM+NAMED++%3Chttp%3A%2F%2Flocalhost%3A3030%2Fsample%2Fdata%2Fdata1538%3E%0AFROM+NAMED++%3Chttp%3A%2F%2Flocalhost%3A3030%2Fsample%2Fdata%2Fdata1537%3E%0AWHERE+%7B%0AGRAPH+g%3Adata1538%0A%7B%0A%3Fs+voc1%3Atotal_c_p+%3Fcomp_yr1.+%0A%3Fs+voc1%3Astate+%3Fstate.%0A%7D%0AGRAPH+g%3Adata1537%0A%7B%0A%3Fs1+voc2%3Atotal_c_p+%3Fcomp_yr2.%0A%3Fs1+voc2%3Astate+%3Fstate+%0A%7D%0A%7D++group+by+%3Fstate+order+by+%3Fstate


e)Comparison of compensation of veterans for each age group irrespective of state

http://localhost:3030/sample/query?output=json&query=PREFIX+xsd%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2001%2FXMLSchema%23%3E%0APREFIX+voc1%3A%3Chttp%3A%2F%2Fdata-gov.tw.rpi.edu%2Fvocab%2Fp%2F1538%2F%3E%0APREFIX+g%3A%3Chttp%3A%2F%2Flocalhost%3A3030%2Fsample%2Fdata%2F%3E%0ASELECT+distinct%0A(SUM(COALESCE(xsd%3Adecimal(%3Fc_60_90)%2C0))+AS+%3Fcompensation_60_90)%0A(SUM(COALESCE(xsd%3Adecimal(%3Fc_30_50)%2C0))+AS+%3Fcompensation_30_50)%0A(SUM(COALESCE(xsd%3Adecimal(%3Fc_100)%2C0))+AS+%3Fcompensation_100)%0A(SUM(COALESCE(xsd%3Adecimal(%3Fc_30)%2C0))+AS+%3Fcompensation_30)+%0AFROM+NAMED++%3Chttp%3A%2F%2Flocalhost%3A3030%2Fsample%2Fdata%2Fdata1538%3E%0AWHERE+%7B%0AGRAPH+g%3Adata1538%0A%7B%0A%3Fs+voc1%3Acompensation_60_90+%3Fc_60_90.+%0A%3Fs+voc1%3Acompensation_30_50+%3Fc_30_50.%0A%3Fs+voc1%3Acompensation_100+%3Fc_100.%0A%3Fs+voc1%3Acompensation_30+%3Fc_30.%0A%7D+%0A%7D

