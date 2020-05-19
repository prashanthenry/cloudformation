# cloudformation
cloud
Hooks": {
      "Logical ID": {
        "Properties": {
            "TrafficRoutingConfig": {
                "Type": "Traffic routing type"
                  "TimeBasedCanary": {
                      "StepPercentage": Integer,
                      "BakeTimeMins": Integer
                }
                "TimeBasedLinear": {
                    "StepPercentage": Integer,
                    "BakeTimeMins": Integer
                }
            },
              "AdditionalOptions": {
                "TerminationWaitTimeInMinutes": Integer
              },
            "LifecycleEventHooks": {
                "BeforeInstall": "FunctionName",
                "AfterInstall": "FunctionName",
                "AfterAllowTestTraffic": "FunctionName",
                "BeforeAllowTraffic": "FunctionName",
                "AfterAllowTraffic": "FunctionName"
            },
            "ServiceRole": {"Ref": "CodeDeployServiceRoleName"},
            "Applications": [{
                "Target": {
                    "Type": "AWS::ECS::Service",
                    "LogicalID": "Resource Logical ID"
                },
                "ECSAttributes": {
                  "TaskDefinitions": ["AWS::ECS::TaskDefinition Resource Logical ID (Blue)", "AWS::ECS::TaskDefinition Resource Logical ID (Green)"],
                  "TaskSets": ["AWS::ECS::TaskSet Resource Logical ID (Blue)", "AWS::ECS::TaskSet Resource Logical ID (Green)"],
                  "TrafficRouting": {
                    "ProdTrafficRoute": {
                      "Type": "AWS::ElasticLoadBalancingV2::Listener",
                      "LogicalID": "Resource Logical ID (Production)"
                    },
                    "TestTrafficRoute": {
                      "Type": "AWS::ElasticLoadBalancingV2::Listener",                
                      "LogicalID": "Resource Logical ID (Test)"             
                    },
                    "TargetGroups": [
                      "AWS::ElasticLoadBalancingV2::TargetGroup Resource Logical ID (Blue)",
                      "AWS::ElasticLoadBalancingV2::TargetGroup Resource Logical ID (Green)"
                    ]
                  }
                }
              }
        ]
      },
        "Type": "AWS::CodeDeploy::BlueGreen"
    }
