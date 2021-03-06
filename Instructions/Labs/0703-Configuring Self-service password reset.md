# Practice Lab - Configuring Self-service password reset (SSPR) for user accounts in Azure AD

## Summary

In this lab, you will practice configuring and testing SSPR and password writeback to AD DS.

### Scenario

The Help Desk has indicated that a large number of support tickets are related to password resets. You have been asked to setup a way for users to reset their password on their own. The process should reset both their Azure AD and AD DS password. 

#### Task 1: Configure password writeback

1.  On **LON-SVR1**, on the desktop, double-click **Azure AD Connect**.

2.  On the **Welcome to Azure AD Connect** page, select **Configure**.

3.  On the **Additional tasks** page, select **Customize synchronization
    options**, and then select **Next**.

4.  On the **Connect to Azure AD** page, if needed type
    **SYNC\@yourtenant.onmicrosoft.com** in the **USERNAME** text box, type
    **Pa55w.rd12345** in the **PASSWORD** text box, and then select **Next**.

5.  On the **Connect to your directories** page, select **Next**.

6.  On the **Domain and OU filtering** page, select **Next**.

7.  On the **Optional features** page, select **Password writeback**, and then
    select **Next**.

8.  On the **Ready to configure** page, select **Configure**.

9.  On the **Configuration complete** page, select **Exit**.

10. Switch to **LON-DC1**. In Microsoft Edge, navigate to **Azure Active Directory**
    in the Azure portal, logged in as the MOD administrator account.

13. In the left navigation pane, select **Password reset**.

14. In the Password reset – Properties window, select **All** to enable
    self-service password reset to all users. Select **Save**.

15. On the **Password reset – Properties** blade, select **Authentication
    methods**.

16. For the methods available to users, ensure that **Mobile Phone** and
    **Email** are selected, and then select **Security Questions**.

17. For the **number of questions required to register**, select **3**.

18. For the **number of questions required to reset**, select **3**.

19. In the **Select security questions** section, select **No security questions
    configured**, then select **Predefined**, select three questions of your
    choice, and then select **OK** twice.

20. Select **Save**.

21. Select on **Registration.** Select **No** for **Require users to register when
    signing in**, and the select **Save**.

22. In the middle pane, select **On-premises integration**.

23. Verify that your on-premises writeback client is running and select **Yes**
    for the **Write back passwords to your on-premises directory** option. Select
    **Save**.

24. Close the Internet Explorer browser window, and then reopen it.

#### Task 2: Configure self-service password reset

1.  Switch to **LON-CL3** and sign in as **Abbi\@yourtenant.onmicrosoft.com** 
    with the password **Pa55w.rd**.

2.  Open Microsoft Edge and browse to **https://myapps.microsoft.com**. 

4.  On the **Microsoft** page, select on the **Abbi** account in the top right
    corner, and then select **Profile**.

5.  Select **Set up self service password reset**.

6.  On the **don’t lose access to your account** page, select **Set it up now**
    for the **Authentication Phone** option.

7.  Choose your country or region, type your mobile phone number, and then select
    **text me**.

8.  Type the number that you receive in a text message in the text box below,
    and then select **verify**.

9.  Select **Set it up now** for the **Authentication Email** option. Type your
    email address that you easily access. Select **email me**.

    _Note: you will need to use an e-mail address other than the tenant domain 
    provided for this lab. If one is not available, you can skip the e-mail 
    verification and continue with step 11._

10. Sign in to your email account, read the code, type it in the verification
    field, and then select **Verify**. Note: If you don’t find a message with a
    code in your inbox, check the junk folder.

11. On the line for **Security Questions are not setup**, select **Set it up now**. Choose
    the three security questions and enter in any answer. Select **Save**.

12. On the **don’t lose access to your account!** page, select **Finish**.

13. On the **Microsoft Azure** page, select on the **Abbi** account, and then
    select **Profile**.

13. In the Azure portal, select **Change password**.

14. On the **change password** page, in the **Old password** text box, type
    **Pa55w.rd**, in the **Create new password** and the **Confirm new
    password** text boxes, type **MDA101!!** and then select **Submit**.

15. Wait until the Microsoft Azure profile portal appears, and then close the
    Internet Explorer browser window.

#### Task 3: Verify password writeback

1.  Ensure that you are signed in to LON-SVR1.

2.  Restore the Windows PowerShell window from the desktop.

3.  At the Windows PowerShell command prompt, type the following commands, and
    then press Enter after each command:

```
Import-Module ADSync

Start-ADSyncSyncCycle –PolicyType Delta

```
4.  Wait for approximately 3-4 minutes.

5.  Minimize Windows PowerShell, and then switch to **LON-CL1** and **Sign out**.

6.  Try to sign in to LON-CL1 as **Adatum\\Abbi** with the password
    **Pa55w.rd**.

7.  Ensure that you get the message that the user name or password is incorrect.

8.  Try to sign in to LON-CL1 as **Adatum\\Abbi** with the password
    **MDA101!!**. You should be able to sign in. This confirms that the password
    you changed in the Azure portal is written back to your local Active
    Directory Domain Services (AD DS).

**END OF LAB**