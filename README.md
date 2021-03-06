# Cloud-Pub-Sub

## Create a Function
  <ul>
  <b>Create a Directory and move in that directory</b>
  <p>mkdir gcf_hello<br>cd gcf_hello</p>
  <b>create and open index.js</b>
  <p>nano index.js</p>
  </ul>
  
## Create a cloud storage bucket
  <ul>
  <p>gsutil mb -p [Project ID] gs://{bucket name}</p>
  </ul>
  
## Deploy your function
  <ul>
  <b>Deploy the function to a pub/sub topic named hello_world</b>
  <p>gcloud functions deploy helloWorld \<br>
  --stage-bucket [BUCKET_NAME] \<br>
  --trigger-topic hello_world \<br>
    --runtime nodejs8</p>
  <b>Verify the status of the function.</b>
  <p>gcloud functions describe helloWorld</p>
  </ul>
  
## Test the function
  <ul>
  <b>Create a message test of the function.</b>
  <p>DATA=$(printf 'Hello World!'|base64) && gcloud functions call helloWorld --data '{"data":"'$DATA'"}'</p>
  </ul>
  
## View logs
  <ul>
  <p>gcloud functions logs read helloWorld</p>
  </ul>
  
## Pub/Sub topics
  <ul>
  <b>Create a pub/sub Topic called Arish</b>
  <p>gcloud pubsub topics create Arish</p>
  <b>To see the topics</b>
  <p>gcloud pubsub topics list</p>
  <b>Deleting Topics Arish</b>
  <p>gcloud pubsub topics delete Arish</p>
  </ul>
  
## Pub/Sub subscriptions
  <ul>
  <b>Create a subscription called mySubscription</b>
  <p>gcloud pubsub subscriptions create --topic Arish mySubscription</p>
  <b>cmd to list all the subscriptions</b>
  <p>gcloud pubsub topics list-subscriptions Arish</p>
  <b>Delete mySubscriptions</b>
  <p>gcloud pubsub subscriptions delete mySubscriptions</p>
  </ul>
  
## Pub/Sub Publishing and Pulling a Single Message
  <ul>
  <b>Publish the Message "Hello" to the topic you created previously(Arish)</b>
  <p>gcloud pubsub topics publish Arish --message "Hello"</p>
  <b>to pull the messages you just published from the Pub/Sub topic</b>
  <p>gcloud pubsub subscriptions pull mySubscription --auto-ack</p>
  
  <i>Now you can publish more messages and then pull them. But on pulling only one message will be output.</i>
  <ul>
    <li>Using the pull command without any flags will output only one message, even if you are subscribed to a topic that has more held in it.</li>
    <li><Once an individual message has been outputted from a particular subscription-based pull command, you cannot access that message again with the pull command.</li>
  </ul>
  </ul>
  
## Pub/Sub pulling all the messages from subscriptions
  <ul>
  <b>Add message to your Topic</b>
  <p>gcloud pubsub topics publish Arish --message "Try1"</p>
  <p>gcloud pubsub topics publish Arish --message "Try2"</p>
  <b>Add a flag to your command so you can output all two messages in one request. You may have not noticed, but you have actually been using a flag this entire time: the --auto-ack part of the pull command is a flag that has been formatting your messages into the neat boxes that you see your pulled messages in.

limit is another flag that sets an upper limit on the number of messages to pull.

Wait a minute to let the topics get created. Run the pull command with the limit flag: </b>
  <p>gcloud pubsub subscriptions pull mySubscription --auto-ack --limit=2</p>
  </ul>
