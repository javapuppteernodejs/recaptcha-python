# How to Solve reCAPTCHA by Using Python and GO
![](https://assets.capsolver.com/prod/images/post/2024-04-26/b88d53aa-367f-478d-93e8-4da580191d22.png)


reCAPTCHA, developed by Google, is a widely used security measure implemented by websites to protect against automated bots. It presents users with challenges to verify their human identity. In this article, we will explore how to solve reCAPTCHA challenges programmatically using Python and Go. We will cover both reCAPTCHA v2 and v3, providing you with the knowledge and tools to overcome these security measures in your web scraping projects.



## What is reCAPTCHA?
reCAPTCHA offers robust protection for websites, effectively preventing fraudulent activities and abuse while maintaining user convenience. Powered by an intelligent risk assessment engine and adaptive challenges, it effectively deters malicious software and ensures smooth access for legitimate users. With a track record of over a decade, reCAPTCHA actively defends data integrity for countless websites. Its seamless approach effortlessly identifies and blocks bots and automated attacks, while still allowing genuine users to navigate without disruption. Leveraging continuous machine learning, reCAPTCHA's adaptive algorithms analyze user interactions and bot behaviors, surpassing the limitations of traditional challenge-based bot detection methods.


**There are several versions of reCAPTCHA:**

reCAPTCHA, developed by Google, comes in several versions, each designed to differentiate between humans and bots in varying ways:

- **reCAPTCHA v1**: The initial version required users to decipher distorted text and input it into a text box.
- **reCAPTCHA v2**: This version introduces a checkbox for users to confirm their human identity. Sometimes, it may also prompt users to select specific images from a grid.
- **reCAPTCHA v3**: Unlike its predecessors, this version operates in the background, analyzing user behavior to assign a score indicating the likelihood of human or bot activity. It offers a seamless experience, requiring no direct interaction from the user.

In this article, our focus will be on solving reCAPTCHA V2 and V3. Those version typically displays a checkbox with the prompt 'I am not a robot' or may appear as an invisible badge, aiming to distinguish genuine users from bots. Here's how it looks in action:

![](https://assets.capsolver.com/prod/images/post/2023-05-12/1786afea-e28f-4f1a-92e2-7fab7b2a81c8.gif)"


## The Best reCAPTCHA Solver: Capsolver

[Capsolver](https://www.capsolver.com/) stands out as one of the top reCAPTCHA solvers available in the market. Offering a combination of affordability, speed, and reliability, Capsolver utilizes AI-powered Captcha Solving Algorithms, resulting in faster solving speeds and reduced costs. This exceptional solution ensures an excellent developer experience when dealing with reCAPTCHA challenges.

### Why Choose Capsolver?

**Affordable and Fast:**
Capsolver offers competitive pricing, making it one of the most cost-effective options for solving reCAPTCHAs. With its AI-powered algorithms, it achieves faster solving speeds, saving valuable time.

**High Reliability:**
Capsolver boasts the fastest update speed among similar providers, ensuring that you have access to the most up-to-date and accurate captcha solving technology. This reliability ensures a smooth and uninterrupted solving experience.

**Risk-Free Solution:**
With Capsolver, you only pay for successfully solved captchas. Their strict cooperation review process ensures that any illegal activities are swiftly identified and banned, providing a secure and trustworthy platform for solving reCAPTCHAs.

**AI-Powered Automation:**
Capsolver leverages the power of artificial intelligence to provide fully automated captcha solving. This eliminates the need for manual intervention, streamlining the solving process and enhancing efficiency.

**Compatibility with Popular Services:**
Capsolver seamlessly works with APIs of popular manual captcha recognition services, ensuring compatibility with various platforms and systems. This flexibility allows for easy integration into your existing workflows.

**Diverse Solutions:**
In addition to its API service, Capsolver also offers a Chrome extension, expanding its capabilities and providing more options for solving reCAPTCHAs. This versatility caters to different user preferences and requirements.

**Trusted by a Wide Range of Platforms:**
With over 1000+ platforms integrating Capsolver's API, it has gained the trust and confidence of numerous businesses and developers. This extensive adoption attests to the reliability and effectiveness of the Capsolver solution.


## How To Solve reCAPTCHA v3-API Guide

### ReCaptchaV3Task

ReCaptchaV3Task is a task type that requires your own proxies to work. It's ideal for those who have a pool of reliable proxies at their disposal. The usage of personal proxies allows for greater control and customization over the solving process.

```python
# pip install --upgrade capsolver
# export CAPSOLVER_API_KEY='...'

import capsolver
# capsolver.api_key = "..."
solution = capsolver.solve({
    "type": "ReCaptchaV3Task",
    "websiteURL": "https://www.google.com/recaptcha/api2/demo",
    "websiteKey": "6Le-wvkSAAAAAPBMRTvw0Q4Muexq9bi0DJwx_kl-",
    "proxy":"ip:port:user:pass", ...
})
```

### ReCaptchaV3TaskProxyLess
If you don't have access to proxies or prefer not to use them, ReCaptchaV3TaskProxyLess is a perfect choice. It leverages the server's built-in proxy, making the process more streamlined and user-friendly.
```python
# pip install --upgrade capsolver
# export CAPSOLVER_API_KEY='...'

import capsolver

# capsolver.api_key = "..."
solution = capsolver.solve({
    "type": "ReCaptchaV3TaskProxyLess",
    "websiteURL": "https://www.google.com/recaptcha/api2/demo",
    "websiteKey": "6Le-wvkSAAAAAPBMRTvw0Q4Muexq9bi0DJwx_kl-", ...
})
```


### Step 1 : Creating a Task

To start the process, you need to create a recognition task using the `createTask` method.

Here's an example request:

```json
POST https://api.capsolver.com/createTask

{
  "clientKey":"yourapiKey",
  "task": {
    "type":"ReCaptchaV3Task",
    "websiteURL":"https://antcpt.com/score_detector",
    "websiteKey":"6LcR_okUAAAAAPYrPe-HK_0RULO1aZM15ENyM-Mf",
    "pageAction": "homepage",
    "proxy":"yourproxy"
  }
}
```
Once the task is successfully submitted, you'll receive a Task ID in the response:

```json
{
  "errorId": 0,
  "errorCode": "",
  "errorDescription": "",
  "taskId": "61138bb6-19fb-11ec-a9c8-0242ac110006"
}
```
### Step 2 : Getting Results

Once you have the Task ID, you can use it to retrieve the solution. Submit the Task ID with the getTaskResult method. The results should be ready within an interval of 1s to 10s.

Here's an example request:
```json
POST https://api.capsolver.com/getTaskResult
Host: api.capsolver.com
Content-Type: application/json

{
  "clientKey":"YOUR_API_KEY",
  "taskId": "TASKID OF CREATETASK" //ID created by the createTask method
}
```
The response will include the solution token:
```json
{
  "errorId": 0,
  "errorCode": null,
  "errorDescription": null,
  "solution": {
    "userAgent": "xxx",
    "expireTime": 1671615324290,
    "gRecaptchaResponse": "3AHJ....."
  },
  "status": "ready"
}
```
In the response, 'solution' contains the 'userAgent', the expiration time of the token 'expireTime', and the solution token 'gRecaptchaResponse'. After the captcha has been solved, you can check the captcha token by sending the token to the site, example:

```json
var request = require('request');

var options = {
  method: 'POST',
  url: 'https://antcpt.com/score_detector/verify.php',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({ 'g-recaptcha-response': 'here the token of capsolver' }),
};

request(options, function (error, response) {
  if (error) throw new Error(error);
  console.log(response.body);
});
```

> More about How To **Solve reCAPTCHA v2**, you can refer to this [Documenatation](https://docs.capsolver.com/guide/captcha/ReCaptchaV2.html)

## How to Solve reCAPTCHA by Using Python and GO
### Sample Code for reCAPTCHA v2
```python
# pip install requests
import requests
import time

# TODO: set your config
api_key = "YOUR_API_KEY"  # your api key of capsolver
site_key = "6Le-wvkSAAAAAPBMRTvw0Q4Muexq9bi0DJwx_mJ-"  # site key of your target site
site_url = "https://www.google.com/recaptcha/api2/demo"  # page url of your target site


def capsolver():
    payload = {
        "clientKey": api_key,
        "task": {
            "type": 'ReCaptchaV2TaskProxyLess',
            "websiteKey": site_key,
            "websiteURL": site_url
        }
    }
    res = requests.post("https://api.capsolver.com/createTask", json=payload)
    resp = res.json()
    task_id = resp.get("taskId")
    if not task_id:
        print("Failed to create task:", res.text)
        return
    print(f"Got taskId: {task_id} / Getting result...")

    while True:
        time.sleep(3)  # delay
        payload = {"clientKey": api_key, "taskId": task_id}
        res = requests.post("https://api.capsolver.com/getTaskResult", json=payload)
        resp = res.json()
        status = resp.get("status")
        if status == "ready":
            return resp.get("solution", {}).get('gRecaptchaResponse')
        if status == "failed" or resp.get("errorId"):
            print("Solve failed! response:", res.text)
            return


token = capsolver()
print(token)
```
```go
package main

import (
	"bytes"
	"context"
	"encoding/json"
	"errors"
	"fmt"
	"io"
	"net/http"
	"time"
)

type capSolverResponse struct {
	ErrorId          int32          `json:"errorId"`
	ErrorCode        string         `json:"errorCode"`
	ErrorDescription string         `json:"errorDescription"`
	TaskId           string         `json:"taskId"`
	Status           string         `json:"status"`
	Solution         map[string]any `json:"solution"`
}

func capSolver(ctx context.Context, apiKey string, taskData map[string]any) (*capSolverResponse, error) {
	uri := "https://api.capsolver.com/createTask"
	res, err := request(ctx, uri, map[string]any{
		"clientKey": apiKey,
		"task":      taskData,
	})
	if err != nil {
		return nil, err
	}
	if res.ErrorId == 1 {
		return nil, errors.New(res.ErrorDescription)
	}

	uri = "https://api.capsolver.com/getTaskResult"
	for {
		select {
		case <-ctx.Done():
			return res, errors.New("solve timeout")
		case <-time.After(time.Second):
			break
		}
		res, err = request(ctx, uri, map[string]any{
			"clientKey": apiKey,
			"taskId":    res.TaskId,
		})
		if err != nil {
			return nil, err
		}
		if res.ErrorId == 1 {
			return nil, errors.New(res.ErrorDescription)
		}
		if res.Status == "ready" {
			return res, err
		}
	}
}

func request(ctx context.Context, uri string, payload interface{}) (*capSolverResponse, error) {
	payloadBytes, err := json.Marshal(payload)
	if err != nil {
		return nil, err
	}
	req, err := http.NewRequestWithContext(ctx, "POST", uri, bytes.NewReader(payloadBytes))
	if err != nil {
		return nil, err
	}
	req.Header.Set("Content-Type", "application/json")
	client := &http.Client{}
	resp, err := client.Do(req)
	if err != nil {
		return nil, err
	}
	defer resp.Body.Close()
	responseData, err := io.ReadAll(resp.Body)
	if err != nil {
		return nil, err
	}
	capResponse := &capSolverResponse{}
	err = json.Unmarshal(responseData, capResponse)
	if err != nil {
		return nil, err
	}
	return capResponse, nil
}

func main() {
	apikey := "YOUR_API_KEY"
	ctx, cancel := context.WithTimeout(context.Background(), time.Second*120)
	defer cancel()

	res, err := capSolver(ctx, apikey, map[string]any{
		"type":       "ReCaptchaV2TaskProxyLess",
		"websiteURL": "https://www.google.com/recaptcha/api2/demo",
		"websiteKey": "6Le-wvkSAAAAAPBMRTvw0Q4Muexq9bi0DJwx_mJ-",
	})
	if err != nil {
		panic(err)
	}
	fmt.Println(res.Solution["gRecaptchaResponse"])
}
```

### Sample Code for reCAPTCHA v3
```python
# pip install requests
import requests
import time

# TODO: set your config
api_key = "YOUR_API_KEY"  # your api key of capsolver
site_key = "6Le-wvkSAAAAAPBMRTvw0Q4Muexq9bi0DJwx_kl-"  # site key of your target site
site_url = "https://www.google.com"  # page url of your target site


def capsolver():
    payload = {
        "clientKey": api_key,
        "task": {
            "type": 'ReCaptchaV3TaskProxyLess',
            "websiteKey": site_key,
            "websiteURL": site_url
        }
    }
    res = requests.post("https://api.capsolver.com/createTask", json=payload)
    resp = res.json()
    task_id = resp.get("taskId")
    if not task_id:
        print("Failed to create task:", res.text)
        return
    print(f"Got taskId: {task_id} / Getting result...")

    while True:
        time.sleep(1)  # delay
        payload = {"clientKey": api_key, "taskId": task_id}
        res = requests.post("https://api.capsolver.com/getTaskResult", json=payload)
        resp = res.json()
        status = resp.get("status")
        if status == "ready":
            return resp.get("solution", {}).get('gRecaptchaResponse')
        if status == "failed" or resp.get("errorId"):
            print("Solve failed! response:", res.text)
            return


token = capsolver()
print(token)
```
```go
package main

import (
	"bytes"
	"context"
	"encoding/json"
	"errors"
	"fmt"
	"io"
	"net/http"
	"time"
)

type capSolverResponse struct {
	ErrorId          int32          `json:"errorId"`
	ErrorCode        string         `json:"errorCode"`
	ErrorDescription string         `json:"errorDescription"`
	TaskId           string         `json:"taskId"`
	Status           string         `json:"status"`
	Solution         map[string]any `json:"solution"`
}

func capSolver(ctx context.Context, apiKey string, taskData map[string]any) (*capSolverResponse, error) {
	uri := "https://api.capsolver.com/createTask"
	res, err := request(ctx, uri, map[string]any{
		"clientKey": apiKey,
		"task":      taskData,
	})
	if err != nil {
		return nil, err
	}
	if res.ErrorId == 1 {
		return nil, errors.New(res.ErrorDescription)
	}

	uri = "https://api.capsolver.com/getTaskResult"
	for {
		select {
		case <-ctx.Done():
			return res, errors.New("solve timeout")
		case <-time.After(time.Second):
			break
		}
		res, err = request(ctx, uri, map[string]any{
			"clientKey": apiKey,
			"taskId":    res.TaskId,
		})
		if err != nil {
			return nil, err
		}
		if res.ErrorId == 1 {
			return nil, errors.New(res.ErrorDescription)
		}
		if res.Status == "ready" {
			return res, err
		}
	}
}

func request(ctx context.Context, uri string, payload interface{}) (*capSolverResponse, error) {
	payloadBytes, err := json.Marshal(payload)
	if err != nil {
		return nil, err
	}
	req, err := http.NewRequestWithContext(ctx, "POST", uri, bytes.NewReader(payloadBytes))
	if err != nil {
		return nil, err
	}
	req.Header.Set("Content-Type", "application/json")
	client := &http.Client{}
	resp, err := client.Do(req)
	if err != nil {
		return nil, err
	}
	defer resp.Body.Close()
	responseData, err := io.ReadAll(resp.Body)
	if err != nil {
		return nil, err
	}
	capResponse := &capSolverResponse{}
	err = json.Unmarshal(responseData, capResponse)
	if err != nil {
		return nil, err
	}
	return capResponse, nil
}

func main() {
	apikey := "YOUR_API_KEY"
	ctx, cancel := context.WithTimeout(context.Background(), time.Second*120)
	defer cancel()

	res, err := capSolver(ctx, apikey, map[string]any{
		"type":       "ReCaptchaV3TaskProxyLess",
		"websiteURL": "https://www.google.com",
		"websiteKey": "6Le-wvkSAAAAAPBMRTvw0Q4Muexq9bi0DJwx_kl-",
	})
	if err != nil {
		panic(err)
	}
	fmt.Println(res.Solution["gRecaptchaResponse"])
}
```
  
## Wrapping up
Solving reCAPTCHA challenges programmatically using Python and Go, coupled with the powerful Capsolver solution, offers an effective approach for web scraping and automation tasks. By understanding the intricacies of reCAPTCHA v2 and v3 and leveraging the capabilities of Capsolver, developers can overcome these security measures efficiently and reliably. Following the comprehensive guides and code examples provided, you can successfully integrate Capsolver into your Python and Go applications to solve reCAPTCHA challenges seamlessly.

