# Google Cloud Speech API: Qwik Start

 Navigation menu > APIs & services > Credentials: create credentials

 API Key
 AIzaSyACqGWOLs_OtOjDsIEzvPiikOEzgo6KQQk

 ssh to compute engine
 export API_KEY=<YOUR_API_KEY>

 touch request.json
 nano request.json

 {
  "config": {
      "encoding":"FLAC",
      "languageCode": "en-US"
  },
  "audio": {
      "uri":"gs://cloud-samples-tests/speech/brooklyn.flac"
  }
}

curl -s -X POST -H "Content-Type: application/json" --data-binary @request.json \
"https://speech.googleapis.com/v1/speech:recognize?key=${API_KEY}"

curl -s -X POST -H "Content-Type: application/json" --data-binary @request.json \
"https://speech.googleapis.com/v1/speech:recognize?key=${API_KEY}" > result.json



