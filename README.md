# Bitlocker-Recovery-Key-Tool
<!-- wp:paragraph {"style":{"typography":{"fontSize":"18px"}}} -->
<p style="font-size:18px">Have you ever been fumbling around, looking for the Bitlocker recovery key but don't know exactly where to look? - add to that having a user on the phone, anxious to start working.. the struggle is real! <br>This tool will make it extremely easy to fetch the key regardless if the key is stored in AD or Azure AD - from a single tool.<br></p>
<!-- /wp:paragraph -->
![alt text](https://usercontent.one/wp/www.nicklasahlberg.se/wp-content/uploads/2022/03/2022-03-26_11-12-50.png?media=1642934880)
<!-- wp:heading -->
<h2>Prerequisites</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>First things first.. we need to make sure that we have a couple of prerequisites in-place.</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>RSAT (if you have keys stored in AD):<ol><li><strong>Install ADDS RSAT feature</strong>: <em>Add-WindowsCapability -Online -Name 'Rsat.ActiveDirectory.DS-LDS.Tools~~~~0.0.1.0'</em></li><li><strong>Install Bitlocker RSAT feature:</strong> <em>Add-WindowsCapability -Online -Name 'Rsat.BitLocker.Recovery.Tools~~~~0.0.1.0'</em></li></ol></li><li>PowerShell module(s):<ol><li><strong>MSAL.PS</strong> <em>Install-Module MSAL.PS</em></li><li><strong>Microsoft.Identity.Client</strong> <em>Install-Module Microsoft.Identity.Client</em></li><li><strong>AZ.Accounts</strong> <em>Install-Module AZ.Accounts</em><img class="wp-image-1188" style="width: 710px;" src="https://www.nicklasahlberg.se/wp-content/uploads/2022/03/Prereqs.png" alt=""></li></ol></li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Let's rock enroll!</h2>
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
<h3>Register the app</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>We will use an Azure registered app with delegated permissions to execute our MS Graph calls against. The next steps cover how to create the app and delegate the appropriate permissions.</p>
<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol><li><strong>Navigate </strong>to: <a rel="noreferrer noopener" href="https://portal.azure.com" target="_blank"><em>https://portal.azure.com</em></a></li><li><strong>Click</strong>: <em>Azure Active Directory</em></li><li><strong>Click</strong>: <em>App registrations</em></li><li><strong>Click</strong>: <em>New registration</em></li><li><strong>Name</strong>: I will use '<em>Demo-Graph</em>' but you may name the app differently</li><li><strong>Supported account types</strong>: <em>Accounts in this organizational directory only</em></li><li><strong>Redirect URI (Select a platform)</strong>: <em>Public client/native (mobile and desktop)</em></li><li><strong>Redirect URI (URL)</strong>: <em>https://login.microsoftonline.com/common/oauth2/nativeclient</em></li><li><strong>Click</strong>: <em>Register</em><img class="wp-image-1197" style="width: 800px;" src="https://www.nicklasahlberg.se/wp-content/uploads/2022/03/Reg-app.png" alt=""></li><li><strong>Save </strong>the <em>Application (client) ID</em> in notepad, we will need it later</li><li><strong>Click</strong>: <em>API Permissions</em><img class="wp-image-1200" style="width: 768px;" src="https://www.nicklasahlberg.se/wp-content/uploads/2022/03/Add-a-permission.png" alt=""></li><li><strong>Click</strong>: <em>Microsoft Graph</em><img class="wp-image-1203" style="width: 778px;" src="https://www.nicklasahlberg.se/wp-content/uploads/2022/03/MSGraphper.png" alt=""></li><li><strong>Click</strong>: <em>Delegated permissions</em><img class="wp-image-1201" style="width: 800px;" src="https://www.nicklasahlberg.se/wp-content/uploads/2022/03/Delegated-permissions.png" alt=""></li><li><strong>Search for and mark</strong>: <em>BitlockerKey.Read.All</em></li><li><strong>Search for and mark</strong>: <em>Device.Read.All</em></li><li><strong>Search for and mark</strong>: <em>DeviceManagementConfiguration.Read.All</em></li><li><strong>Click</strong>: <em>Add permissions</em></li><li><strong>Click</strong>: <em>Grant admin consent for</em>...<img class="wp-image-1202" style="width: 724px;" src="https://www.nicklasahlberg.se/wp-content/uploads/2022/03/Grant.png" alt=""></li><li><strong>Click</strong>: <em>Yes</em></li><li>Make sure that the permissions have been granted accordingly<img class="wp-image-1211" style="width: 706px;" src="https://www.nicklasahlberg.se/wp-content/uploads/2022/03/Granted.png" alt=""></li><li>Now <strong>navigate </strong>to <a rel="noreferrer noopener" href="https://aad.portal.azure.com/" target="_blank"><em>https://aad.portal.azure.com/</em></a></li><li><strong>Click</strong>: <em>Azure Active Directory</em></li><li><strong>Save </strong>the <em>Tenant ID</em> in notepad, we will need it later</li></ol>
<!-- /wp:list -->

<!-- wp:heading {"level":3} -->
<h3>Download the tool</h3>
<!-- /wp:heading -->

<!-- wp:list {"ordered":true} -->
<ol><li>Download the tool from: <a href="https://github.com/NicklasAhlberg/Bitlocker-Recovery-Key-Tool">NicklasAhlberg/Bitlocker-Recovery-Key-Tool (github.com)</a></li><li>Make sure you download the latest version from the <em>releases </em>section<img class="wp-image-1209" style="width: 328px;" src="https://www.nicklasahlberg.se/wp-content/uploads/2022/03/Releases.png" alt=""></li><li>Extract the zip-file and make sure that following three (3) files are in the same directory<br><img class="wp-image-1210" style="width: 288px;" src="https://www.nicklasahlberg.se/wp-content/uploads/2022/03/Files.png" alt=""></li><li><strong>Open: </strong><em>config.txt</em> and paste the clientID and tenantID from notepad</li><li><strong>Save: </strong><em>config.txt</em></li></ol>
<!-- /wp:list -->

<!-- wp:heading {"level":3} -->
<h3>Run the tool</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Run the tool by executing: <em>Bitlocker Recovery Key Tool.exe</em><img class="wp-image-1184" style="width: 666px;" src="https://www.nicklasahlberg.se/wp-content/uploads/2022/03/Second.gif" alt=""></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->
