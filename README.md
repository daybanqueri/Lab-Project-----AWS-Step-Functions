# Lab-Project-----AWS-Step-Functions

<img width="607" height="752" alt="stepfunctions_graph-2" src="https://github.com/user-attachments/assets/033b6411-4475-4200-afba-20bfb9efbce3" />


{
  "Comment": "A description of my state machine",
  "StartAt": "Checar Estoque",
  "States": {
    "Checar Estoque": {
      "Type": "Task",
      "Resource": "arn:aws:states:::lambda:invoke",
      "Parameters": {
        "FunctionName": "arn:aws:lambda:us-east-1:606010181329:function:MyFirstFunction:$LATEST",
        "Payload.$": "$"
      },
      "ResultPath": "$",
      "Retry": [
        {
          "ErrorEquals": [
            "Lambda.ServiceException",
            "Lambda.AWSLambdaException",
            "Lambda.SdkClientException",
            "Lambda.TooManyRequestsException"
          ],
          "IntervalSeconds": 1,
          "MaxAttempts": 3,
          "BackoffRate": 2,
          "JitterStrategy": "FULL"
        }
      ],
      "Next": "Escolha"
    },
    "Escolha": {
      "Type": "Choice",
      "Choices": [
        {
          "Variable": "$.paymentApproved",
          "BooleanEquals": true,
          "Next": "Criar Ordem"
        }
      ],
      "Default": "Enviar Mensagem Falta de Estoque"
    },
    "Criar Ordem": {
      "Type": "Task",
      "Resource": "arn:aws:states:::lambda:invoke",
      "Parameters": {
        "FunctionName": "arn:aws:lambda:us-east-1:606010181329:function:MyFirstFunction:$LATEST",
        "Payload.$": "$"
      },
      "ResultPath": "$",
      "Retry": [
        {
          "ErrorEquals": [
            "Lambda.ServiceException",
            "Lambda.AWSLambdaException",
            "Lambda.SdkClientException",
            "Lambda.TooManyRequestsException"
          ],
          "IntervalSeconds": 1,
          "MaxAttempts": 3,
          "BackoffRate": 2,
          "JitterStrategy": "FULL"
        }
      ],
      "Next": "Gerar Nota"
    },
    "Gerar Nota": {
      "Type": "Task",
      "Resource": "arn:aws:states:::lambda:invoke",
      "Parameters": {
        "FunctionName": "arn:aws:lambda:us-east-1:606010181329:function:MyFirstFunction:$LATEST",
        "Payload.$": "$"
      },
      "ResultPath": "$",
      "Retry": [
        {
          "ErrorEquals": [
            "Lambda.ServiceException",
            "Lambda.AWSLambdaException",
            "Lambda.SdkClientException",
            "Lambda.TooManyRequestsException"
          ],
          "IntervalSeconds": 1,
          "MaxAttempts": 3,
          "BackoffRate": 2,
          "JitterStrategy": "FULL"
        }
      ],
      "Next": "Solicitar Pagamento"
    },
    "Solicitar Pagamento": {
      "Type": "Task",
      "Resource": "arn:aws:states:::lambda:invoke",
      "Parameters": {
        "FunctionName": "arn:aws:lambda:us-east-1:606010181329:function:MyFirstFunction:$LATEST",
        "Payload.$": "$"
      },
      "ResultPath": "$",
      "Retry": [
        {
          "ErrorEquals": [
            "Lambda.ServiceException",
            "Lambda.AWSLambdaException",
            "Lambda.SdkClientException",
            "Lambda.TooManyRequestsException"
          ],
          "IntervalSeconds": 1,
          "MaxAttempts": 3,
          "BackoffRate": 2,
          "JitterStrategy": "FULL"
        }
      ],
      "Next": "Enviar Mensagem"
    },
    "Enviar Mensagem": {
      "Type": "Task",
      "Resource": "arn:aws:states:::lambda:invoke",
      "Parameters": {
        "FunctionName": "arn:aws:lambda:us-east-1:606010181329:function:MyFirstFunction:$LATEST",
        "Payload.$": "$"
      },
      "ResultPath": "$",
      "Retry": [
        {
          "ErrorEquals": [
            "Lambda.ServiceException",
            "Lambda.AWSLambdaException",
            "Lambda.SdkClientException",
            "Lambda.TooManyRequestsException"
          ],
          "IntervalSeconds": 1,
          "MaxAttempts": 3,
          "BackoffRate": 2,
          "JitterStrategy": "FULL"
        }
      ],
      "Next": "Êxito"
    },
    "Êxito": {
      "Type": "Succeed"
    },
    "Enviar Mensagem Falta de Estoque": {
      "Type": "Task",
      "Resource": "arn:aws:states:::lambda:invoke",
      "Parameters": {
        "FunctionName": "arn:aws:lambda:us-east-1:606010181329:function:MyFirstFunction:$LATEST",
        "Payload.$": "$"
      },
      "ResultPath": "$",
      "Retry": [
        {
          "ErrorEquals": [
            "Lambda.ServiceException",
            "Lambda.AWSLambdaException",
            "Lambda.SdkClientException",
            "Lambda.TooManyRequestsException"
          ],
          "IntervalSeconds": 1,
          "MaxAttempts": 3,
          "BackoffRate": 2,
          "JitterStrategy": "FULL"
        }
      ],
      "Next": "Falha"
    },
    "Falha": {
      "Type": "Fail"
    }
  }
}
