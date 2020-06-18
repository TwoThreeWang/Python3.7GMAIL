# Python3 GMAIL
# Send emails by gmail with python 3 群发邮件
# If password doesn't work, and you know you entered it right. Enable gmail 2 factor authentication, then create app password for python. 



import smtplib

import pandas as pd

datafile = 'C:/Users/User1/Desktop/information.csv'

data = pd.read_csv(datafile)

emails = data.iloc[:, 0]

names = data.iloc[:, 1]

contents = data.iloc[:, 2]

corp_name = data.iloc[:, 3]

gmail_sender = 'name@gmail.com'

gmail_passwd = 'password'


server = smtplib.SMTP('smtp.gmail.com', 587)

server.ehlo()

server.starttls()

server.login(gmail_sender, gmail_passwd)


for i in range(len(emails)):

    TO = emails[i]
    
    SUBJECT = str(corp_name[i])
    
    TEXT = 'Dear ' + str(names[i]) + '\nHi, This is a message from python'
    
    BODY = '\r\n'.join(['To: %s' % TO,
    
                        'From: %s' % gmail_sender,
                        
                        'Subject: %s' % SUBJECT,
                        
                        '', TEXT])
                        
    try:
    
        server.sendmail(gmail_sender, [TO], BODY)
        
        print('email sent')
        
    except:
    
        print('error sending mail')

server.quit()
