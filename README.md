# EC2 & CloudWatch Monitoring

## Project Objective

Built a hands-on AWS monitoring and incident-response lab using Amazon EC2 and Amazon CloudWatch.

The project demonstrates how to:
- Monitor EC2 CPU utilization
- Configure a CloudWatch alarm
- Send an SNS notification when CPU usage is high
- Investigate the cause of a CPU spike
- Stop the process causing excessive CPU usage
- Verify that the server returns to normal

## AWS Services Used

- Amazon EC2
- Amazon CloudWatch
- Amazon SNS

## Monitoring Configuration

- Metric: CPUUtilization
- Statistic: Average
- Period: 5 minutes
- Alarm threshold: CPU utilization > 70%
- Alarm name: ec2-cpu-high-70
- Notification: Amazon SNS email

## Incident Simulation

A CPU load was intentionally generated on the EC2 instance using:

`yes > /dev/null &`

The `top` command was then used to investigate CPU usage and identify the `yes` process consuming approximately 100% CPU.

The process was stopped using:

`pkill yes`

After the process was stopped, CPU utilization returned to normal.

## Alarm Response

CloudWatch recorded the following alarm lifecycle:

`OK → IN ALARM → OK`

The SNS action was successfully executed when the alarm entered the alarm state.

## Troubleshooting Workflow

```text
CloudWatch detects high CPU
        ↓
Alarm changes to IN ALARM
        ↓
SNS notification is triggered
        ↓
Investigate EC2 with top
        ↓
Identify high-CPU process
        ↓
Stop the process
        ↓
CPU returns to normal
        ↓
Alarm returns to OK
