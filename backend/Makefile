all: build deploy
ORIGIN ?= *
STACKNAME ?= aws-serverless-shopping-cart

build:
	@echo "Building template $(TEMPLATE).yaml..."
	@samlocal build -t $(TEMPLATE).yaml

deploy:  # s3 bucket still needed for layer
	@echo "Deploying stack $(STACKNAME)-$(TEMPLATE)..."
	@samlocal deploy --capabilities CAPABILITY_NAMED_IAM --stack-name $(STACKNAME)-$(TEMPLATE) --s3-bucket $(S3_BUCKET) --no-fail-on-empty-changeset

tests:
	py.test -v

delete:
	@awslocal cloudformation delete-stack --stack-name $(STACKNAME)-$(TEMPLATE)
	@echo "Waiting for stack $(STACKNAME)-$(TEMPLATE) to be deleted..."
	@awslocal cloudformation wait stack-delete-complete --stack-name $(STACKNAME)-$(TEMPLATE)

.PHONY: build package deploy delete
