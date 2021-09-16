# QR-code-generator
QR code generator with html

</li></ol><blockquote><p>To Send Direct Message without any user intervention you can visit <a href="https://aboutreact.com/react-native-bridge-send-direct-sms-from-react-native-app/" target="_blank" rel="noopener">React Native Bridge Example to Send Direct SMS from React Native App</a></p></blockquote><h2><span id="To-Send-SMS">To Send SMS</span></h2><pre><code>SendSMS.send(
  {
    // Message body
    body: bodySMS,
    // Recipients Number
    recipients: [mobileNumber],
    // An array of types 
    // "completed" response when using android
    successTypes: ['sent', 'queued'],
  },
  (completed, cancelled, error) =&gt; {
    if (completed) {
      console.log('SMS Sent Completed');
    } else if (cancelled) {
      console.log('SMS Sent Cancelled');
    } else if (error) {
      console.log('Some error occured');
    }
  },
);</code></pre><p>In this example of sending a Text SMS from React Native App, we will send the SMS by clicking on a button using  <code>react-native-sms</code> library. So let&#8217;s get started.</p><h2><span id="To-Make-a-React-Native-App">To Make a React Native App</span></h2><p><a href="https://aboutreact.com/getting-started-with-react-native/" target="_blank" rel="noopener noreferrer">Getting started with React Native</a> will help you to know more about the way you can make a React Native project. We are going to use react-native init to make our React Native App. Assuming that you have node installed, you can use npm to install the <code>react-native-cli</code> command line utility. Open the terminal and go to the workspace and run</p><pre><code>npm install -g react-native-cli</code></pre><p>Run the following commands to create a new React Native project</p><pre><code>react-native init ProjectName</code></pre><p>If you want to start a new project with a specific React Native version, you can use the --version argument:</p><pre><code>react-native init ProjectName --version X.XX.X</code></pre><pre><code>react-native init ProjectName --version react-native@next</code></pre><p>This will make a project structure with an index file named App.js in your project directory.</p><h2><span id="Installation-of-Dependency">Installation of Dependency</span></h2><p>To use <code>SendSMS</code> we need to install <code>react-native-sms</code> package. To install this</p><p>Open the terminal and jump into your project</p><pre><code>cd ProjectName</code></pre><p>Run the following command</p><pre><code>npm install react-native-sms --save</code></pre><p>This command will copy all the dependencies into your node_module directory.</p><h2><span id="CocoaPods-Installation">CocoaPods Installation</span></h2><p>After the updation of React Native 0.60, they have introduced <a href="https://aboutreact.com/react-native-autolinking/" target="_blank" rel="noopener noreferrer">autolinking</a> so we do not require to link the library but need to install pods. So to install pods use</p><pre class=""><code>cd ios &amp;&amp; pod install &amp;&amp; cd ..</code></pre><h2><span id="Permission-to-Send-SMS-for-Android">Permission to Send SMS for Android</span></h2><p>We are trying to use the SMS feature so we need to add some permission in <code>AndroidManifest.xml</code> file for Android. For more about the permission, you can see <a href="https://aboutreact.com/react-native-android-permission/" target="_blank" rel="noopener noreferrer">this post</a>.</p><p>So we are going to add the following permissions in the AndroidMnifest.xml</p><pre><code>&lt;uses-permission android:name="android.permission.READ_SMS"/&gt;</code></pre><p><a href="https://aboutreact.com/wp-content/uploads/2018/09/sms_example4.png" target="_blank" rel="noopener noreferrer"><noscript><img   alt="" width="1366" height="666" data-srcset="https://aboutreact.com/wp-content/uploads/2018/09/sms_example4.png 1366w, https://aboutreact.com/wp-content/uploads/2018/09/sms_example4-300x146.png 300w, https://aboutreact.com/wp-content/uploads/2018/09/sms_example4-768x374.png 768w, https://aboutreact.com/wp-content/uploads/2018/09/sms_example4-1024x499.png 1024w"  data-src="https://aboutreact.com/wp-content/uploads/2018/09/sms_example4.png" data-sizes="(max-width: 1366px) 100vw, 1366px" class="aligncenter wp-image-1949 size-full lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==" /><noscript><img class="aligncenter wp-image-1949 size-full" src="https://aboutreact.com/wp-content/uploads/2018/09/sms_example4.png" alt="" width="1366" height="666" srcset="https://aboutreact.com/wp-content/uploads/2018/09/sms_example4.png 1366w, https://aboutreact.com/wp-content/uploads/2018/09/sms_example4-300x146.png 300w, https://aboutreact.com/wp-content/uploads/2018/09/sms_example4-768x374.png 768w, https://aboutreact.com/wp-content/uploads/2018/09/sms_example4-1024x499.png 1024w" sizes="(max-width: 1366px) 100vw, 1366px" /></noscript></noscript><img class="lazyload aligncenter wp-image-1949 size-full" src='data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%201366%20666%22%3E%3C/svg%3E' data-src="https://aboutreact.com/wp-content/uploads/2018/09/sms_example4.png" alt="" width="1366" height="666" data-srcset="https://aboutreact.com/wp-content/uploads/2018/09/sms_example4.png 1366w, https://aboutreact.com/wp-content/uploads/2018/09/sms_example4-300x146.png 300w, https://aboutreact.com/wp-content/uploads/2018/09/sms_example4-768x374.png 768w, https://aboutreact.com/wp-content/uploads/2018/09/sms_example4-1024x499.png 1024w" data-sizes="(max-width: 1366px) 100vw, 1366px" /></a></p><p>Here we have done all the configurations we need.</p><h2><span id="Code-to-Send-Text-SMS">Code to <strong>Send Text SMS</strong></span></h2><p>Now open App.js in any code editor and replace the code with the following code</p><h3><span id="Appjs">App.js</span></h3><pre><code>// Example to Send Text SMS on Button Click in React Native
// https://aboutreact.com/send-text-sms-in-react-native/

// import React in our code
import React, {useState} from 'react';

// import all the components we are going to use
import {
  SafeAreaView,
  StyleSheet,
  View,
  Text,
  TouchableOpacity,
  TextInput,
} from 'react-native';

// import SMS API
import SendSMS from 'react-native-sms';

const App = () =&gt; {
  const [mobileNumber, setMobileNumber] = useState('9999999999');
  const [bodySMS, setBodySMS] = useState(
    'Please follow https://aboutreact.com',
  );

  const initiateSMS = () =&gt; {
    // Check for perfect 10 digit length
    if (mobileNumber.length != 10) {
      alert('Please insert correct contact number');
      return;
    }

    SendSMS.send(
      {
        // Message body
        body: bodySMS,
        // Recipients Number
        recipients: [mobileNumber],
        // An array of types 
        // "completed" response when using android
        successTypes: ['sent', 'queued'],
      },
      (completed, cancelled, error) =&gt; {
        if (completed) {
          console.log('SMS Sent Completed');
        } else if (cancelled) {
          console.log('SMS Sent Cancelled');
        } else if (error) {
          console.log('Some error occured');
        }
      },
    );
  };

  return (
    &lt;SafeAreaView style={styles.container}&gt;
      &lt;View style={styles.container}&gt;
        &lt;Text style={styles.titleText}&gt;
          Example to Send Text SMS on Button Click in React Native
        &lt;/Text&gt;
        &lt;Text style={styles.titleTextsmall}&gt;
          Enter Mobile Number
        &lt;/Text&gt;
        &lt;TextInput
          value={mobileNumber}
          onChangeText={
            (mobileNumber) =&gt; setMobileNumber(mobileNumber)
          }
          placeholder={'Enter Conatct Number to Call'}
          keyboardType="numeric"
          style={styles.textInput}
        /&gt;
        &lt;Text style={styles.titleTextsmall}&gt;
          Enter SMS body
        &lt;/Text&gt;
        &lt;TextInput
          value={bodySMS}
          onChangeText={(bodySMS) =&gt; setBodySMS(bodySMS)}
          placeholder={'Enter SMS body'}
          style={styles.textInput}
        /&gt;
        &lt;TouchableOpacity
          activeOpacity={0.7}
          style={styles.buttonStyle}
          onPress={initiateSMS}&gt;
          &lt;Text style={styles.buttonTextStyle}&gt;
            Send Message
          &lt;/Text&gt;
        &lt;/TouchableOpacity&gt;
      &lt;/View&gt;
    &lt;/SafeAreaView&gt;
  );
};

export default App;

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: 'white',
    padding: 10,
    textAlign: 'center',
  },
  titleText: {
    fontSize: 22,
    textAlign: 'center',
    fontWeight: 'bold',
  },
  titleTextsmall: {
    marginVertical: 8,
    fontSize: 16,
  },
  buttonStyle: {
    justifyContent: 'center',
    marginTop: 15,
    padding: 10,
    backgroundColor: '#8ad24e',
  },
  buttonTextStyle: {
    color: '#fff',
    textAlign: 'center',
  },
  textInput: {
    height: 40,
    borderColor: 'gray',
    borderWidth: 1,
    width: '100%',
    paddingHorizontal: 10,
  },
});</code></pre><h2><span id="To-Run-theReact-Native-App">To Run the React Native App</span></h2><p>Open the terminal again and jump into your project using.</p><pre><code>cd ProjectName</code></pre><p>To run the project on an Android Virtual Device or on real debugging device</p><pre><code>react-native run-android</code></pre><p>or on the iOS Simulator by running (macOS only)</p><pre><code>react-native run-ios</code></pre><p style="text-align: center;"> <a href="https://downloadfile.link/?ps=1602527023" target="_blank" class="emd_dl_green_dark" download>Download Source Code</a></p><h2 style="text-align: center;"><span id="Output-Screenshots">Output Screenshots</span></h2><div style="text-align: center;"><a href="https://aboutreact.com/wp-content/uploads/2019/10/react_native_send_sms1.jpg" target="_blank" rel="noopener noreferrer"><noscript><img   alt="react_native_send_sms1" width="142" height="300" data-srcset="https://aboutreact.com/wp-content/uploads/2019/10/react_native_send_sms1-142x300.jpg 142w, https://aboutreact.com/wp-content/uploads/2019/10/react_native_send_sms1-485x1024.jpg 485w, https://aboutreact.com/wp-content/uploads/2019/10/react_native_send_sms1-768x1621.jpg 768w, https://aboutreact.com/wp-content/uploads/2019/10/react_native_send_sms1-728x1536.jpg 728w, https://aboutreact.com/wp-content/uploads/2019/10/react_native_send_sms1-970x2048.jpg 970w, https://aboutreact.com/wp-content/uploads/2019/10/react_native_send_sms1.jpg 1080w"  data-src="https://aboutreact.com/wp-content/uploads/2019/10/react_native_send_sms1-142x300.jpg" data-sizes="(max-width: 142px) 100vw, 142px" class="alignnone wp-image-9466 size-medium lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==" /><noscript><img class="alignnone wp-image-9466 size-medium" src="https://aboutreact.com/wp-content/uploads/2019/10/react_native_send_sms1-142x300.jpg" alt="react_native_send_sms1" width="142" height="300" srcset="https://aboutreact.com/wp-content/uploads/2019/10/react_native_send_sms1-142x300.jpg 142w, https://aboutreact.com/wp-content/uploads/2019/10/react_native_send_sms1-485x1024.jpg 485w, https://aboutreact.com/wp-content/uploads/2019/10/react_native_send_sms1-768x1621.jpg 768w, https://aboutreact.com/wp-content/uploads/2019/10/react_native_send_sms1-728x1536.jpg 728w, https://aboutreact.com/wp-content/uploads/2019/10/react_native_send_sms1-970x2048.jpg 970w, https://aboutreact.com/wp-content/uploads/2019/10/react_native_send_sms1.jpg 1080w" sizes="(max-width: 142px) 100vw, 142px" /></noscript></noscript><img class="lazyload alignnone wp-image-9466 size-medium" src='data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20142%20300%22%3E%3C/svg%3E' data-src="https://aboutreact.com/wp-content/uploads/2019/10/react_native_send_sms1-142x300.jpg" alt="react_native_send_sms1" width="142" height="300" data-srcset="https://aboutreact.com/wp-content/uploads/2019/10/react_native_send_sms1-142x300.jpg 142w, https://aboutreact.com/wp-content/uploads/2019/10/react_native_send_sms1-485x1024.jpg 485w, https://aboutreact.com/wp-content/uploads/2019/10/react_native_send_sms1-768x1621.jpg 768w, https://aboutreact.com/wp-content/uploads/2019/10/react_native_send_sms1-728x1536.jpg 728w, https://aboutreact.com/wp-content/uploads/2019/10/react_native_send_sms1-970x2048.jpg 970w, https://aboutreact.com/wp-content/uploads/2019/10/react_native_send_sms1.jpg 1080w" data-sizes="(max-width: 142px) 100vw, 142px" /></a>    <a href="https://aboutreact.com/wp-content/uploads/2018/09/2-1.png" target="_blank" rel="noopener noreferrer"><noscript><img   alt="react_native_send_sms2" width="169" height="300" data-srcset="https://aboutreact.com/wp-content/uploads/2018/09/2-1-169x300.png 169w, https://aboutreact.com/wp-content/uploads/2018/09/2-1-768x1365.png 768w, https://aboutreact.com/wp-content/uploads/2018/09/2-1-576x1024.png 576w, https://aboutreact.com/wp-content/uploads/2018/09/2-1.png 1080w"  data-src="https://aboutreact.com/wp-content/uploads/2018/09/2-1-169x300.png" data-sizes="(max-width: 169px) 100vw, 169px" class="alignnone wp-image-1951 size-medium lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==" /><noscript><img class="alignnone wp-image-1951 size-medium" src="https://aboutreact.com/wp-content/uploads/2018/09/2-1-169x300.png" alt="react_native_send_sms2" width="169" height="300" srcset="https://aboutreact.com/wp-content/uploads/2018/09/2-1-169x300.png 169w, https://aboutreact.com/wp-content/uploads/2018/09/2-1-768x1365.png 768w, https://aboutreact.com/wp-content/uploads/2018/09/2-1-576x1024.png 576w, https://aboutreact.com/wp-content/uploads/2018/09/2-1.png 1080w" sizes="(max-width: 169px) 100vw, 169px" /></noscript></noscript><img class="lazyload alignnone wp-image-1951 size-medium" src='data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20viewBox=%220%200%20169%20300%22%3E%3C/svg%3E' data-src="https://aboutreact.com/wp-content/uploads/2018/09/2-1-169x300.png" alt="react_native_send_sms2" width="169" height="300" data-srcset="https://aboutreact.com/wp-content/uploads/2018/09/2-1-169x300.png 169w, https://aboutreact.com/wp-content/uploads/2018/09/2-1-768x1365.png 768w, https://aboutreact.com/wp-content/uploads/2018/09/2-1-576x1024.png 576w, https://aboutreact.com/wp-content/uploads/2018/09/2-1.png 1080w" data-sizes="(max-width: 169px) 100vw, 169px" /></a></div><div></div><p>This is how you can send SMS in React Native. If you have any doubt or you want to share something about the topic you can comment below or <a href="https://aboutreact.com/contact/" target="_blank" rel="noopener noreferrer">contact us here</a>. There will be more posts coming soon. Stay tuned!</p><p>Hope you liked it. 🙂</p>
