# basic-lambda-setup
My template for making a basic lambda function when there's no API call -- such as when the function is triggered by CloudWatch (such as every 15 mins) or by an Alexa command.

For lambda functions triggered by API calls, I use `claudia-api-builder`. My [Party Bot](https://github.com/jkeefe/party-bot) is a simple exapmle of that.

## Base files

I add these to my repo:

- [`.gitignore`](https://gist.github.com/jkeefe/947f17282c06729924fd23180af38258) is my file for ignoreing files.

- [`index.js`](./index.js) is where I build the bot. This will get called by the lambda function.

- [`test.js`](./test.js) is how I run `index.js` locally, to test it:

```
node test.js
```

### Setting Up Claudia

```
npm install claudia --save-dev
```

Here are some important notes about the creation command I'm about to run: 

- I use the full path to claudia because it sometimes doesn't work otherwise
- In this app, the bot runs in `index.js`.
- The "index.handler" in the command below comes from the name of the file `index.js` and the module inside that file `exports.handler`. 
- For permission to run/use the function, I'm using a "role" I've already set up instead of my own credentials. The role was set up in IAM, Amazon's permissions system. More about that in the Claudia [installation documents](https://claudiajs.com/tutorials/installing.html).
- Other arguments for the create command arelisted [here]https://github.com/claudiajs/claudia/blob/master/docs/create.md. 

So this command creates the lambda function initially: 

```
./node_modules/.bin/claudia create --region us-east-1 --handler index.handler --role lambda_basic_execution
```

Any subsequent updates can skip all of that and just use this command:

```
./node_modules/.bin/claudia update
```

