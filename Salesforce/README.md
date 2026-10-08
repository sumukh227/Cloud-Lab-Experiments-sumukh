# Salesforce Experiments

## Experiment 4: Building and Running an Apex Program

### Steps
1. Sign in to your Salesforce Developer account.
2. Click the Gear icon (Setup) in the top-right corner and select Developer Console.
3. In Developer Console, go to File -> New -> Apex Class.
4. Enter the class name as HelloWorldApp and click OK.
5. Add the code:
public class HelloWorldApp {
    public static void sayHello() {
        System.debug('Welcome to Salesforce Apex');
    }
}
6. Press Ctrl + S to save the class.
7. Go to Debug -> Open Execute Anonymous Window.
8. Type the call command:
HelloWorldApp.sayHello();
9. Check the Open Log box and click Execute.
10. In the log tab, check the Debug Only box to view the output message.

---

## Experiment 5: Implementing an Email Service with Attachment in Apex

### Steps
1. Open Developer Console from the Setup menu.
2. Go to File -> New -> Apex Class.
3. Enter the class name as EmailService and click OK.
4. Add the code:
public class EmailService {
    public static void sendEmailWithAttachment(String recipientAddress, String subject, String bodyMessage) {
        Messaging.SingleEmailMessage mail = new Messaging.SingleEmailMessage();
        String[] toAddresses = new String[] { recipientAddress };
        mail.setToAddresses(toAddresses);
        mail.setSubject(subject);
        mail.setPlainTextBody(bodyMessage);

        Messaging.EmailFileAttachment textAttachment = new Messaging.EmailFileAttachment();
        textAttachment.setFileName('SalesforceReport.txt');
        textAttachment.setContentType('text/plain');
        String fileContentStr = 'This is the internal content of your generated text file attachment.\nCreated on: ' + System.now();
        Blob fileBodyBlob = Blob.valueOf(fileContentStr);
        textAttachment.setBody(fileBodyBlob);

        mail.setFileAttachments(new Messaging.EmailFileAttachment[] { textAttachment });
        Messaging.SendEmailResult[] results = Messaging.sendEmail(new Messaging.SingleEmailMessage[] { mail });

        if (results[0].isSuccess()) {
            System.debug('Email with attachment sent successfully to: ' + recipientAddress);
        } else {
            System.debug('Email sending failed: ' + results[0].getErrors()[0].getMessage());
        }
    }
}
5. Press Ctrl + S to save the class.
6. Go to Debug -> Open Execute Anonymous Window.
7. Enter the execution code (replace with your recipient email):
EmailService.sendEmailWithAttachment(
    'your_actual_email@example.com',
    'Apex Mailer with Attachment!',
    'Please check the attached text file generated directly from Salesforce.'
);
8. Check the Open Log box and click Execute.
9. Check the Debug Only box in the log window to confirm the success message.
10. Check your inbox to verify the email and download the attached text file.