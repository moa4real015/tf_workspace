resource "aws_instance" "EC2-Terraform" {
  ami           = "ami-06b0bb707079eb96a"
  instance_type = "t2.micro"
  #security_groups = ["aws_security_group.TF_SG.name"]
  count         = 2

  tags = {
    Name = "EC2-Terraform"
  }
}

# security group using terraform
resource "aws_security_group" "TF_SG" {
  name        = "SG-terraform"
  description = "SG-terraform"
  vpc_id      = "vpc-0e347a02710225bbe"

  ingress {
    description      = "HTTPS"
    from_port        = 443
    to_port          = 443
    protocol         = "tcp"
    cidr_blocks      = ["0.0.0.0/0"]
    ipv6_cidr_blocks = ["::/0"]
  }

  ingress {
    description      = "HTTP"
    from_port        = 80
    to_port          = 80
    protocol         = "tcp"
    cidr_blocks      = ["0.0.0.0/0"]
    ipv6_cidr_blocks = ["::/0"]
  }

  ingress {
    description      = "SSH"
    from_port        = 22
    to_port          = 22
    protocol         = "tcp"
    cidr_blocks      = ["0.0.0.0/0"]
    ipv6_cidr_blocks = ["::/0"]
  }

  egress {
    from_port        = 0
    to_port          = 0
    protocol         = "-1"
    cidr_blocks      = ["0.0.0.0/0"]
    ipv6_cidr_blocks = ["::/0"]
  }

  tags = {
    Name = "TF_SG"
  }
}





