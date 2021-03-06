provider "aws" {
region = "us-east-1"
}

resource "aws_security_group" "allow_sample" {
name        = "allow_sample"
description = "Allow sample traffic"

ingress = [
{
description      = "TLS from VPC"
from_port        = 22
to_port          = 22
protocol         = "tcp"
cidr_blocks      = ["0.0.0.0/0"]
ipv6_cidr_blocks = []
prefix_list_ids  = []
security_groups  = []
self             = false
}
]

egress = [
{
description      = "egress"
from_port        = 22
to_port          = 22
protocol         = "tcp"
cidr_blocks      = ["0.0.0.0/0"]
ipv6_cidr_blocks = ["::/0"]
prefix_list_ids  = []
security_groups  = []
self             = false
}
]

tags = {
Name = "allow_sample"
}
}

resource "aws_instance" "sample" {
ami                    = ami-0bb6af715826253bf
instance_type          = t3.micro" 
vpc_security_group_ids = [aws_security_group.allow_sample.id]

tags = {
Name = sample
}
}
