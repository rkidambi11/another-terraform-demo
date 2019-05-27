#!/usr/bin/env groovy     
/*
#title           :aws-terraform-demo-groovy
#description     :This script will provisioning the AWS Environment
#author		     :Ranga Kidambi
#date            :27/May/2019
#version         :1.0 
#usage		     :It makes VPC and EC2 instance including subnets
#notes           :Install Vim and Emacs to use this script
#==============================================================================
*/

//Inputparamter Checks 
node {
stage('Declarative Pipeline : Input Parameters Check'){	
	def missingParams = false
	
	if(params.Environment==null) {
		println "No Environment parameter value set"
		missingParams = true
	}
	
	if(params.DataCenter==null) {
		println "No DataCenter parameter value set"
		missingParams = true
	}
	
	if(params.GITRepositoryTerraformName==null) {
		println "No GITRepositoryTerraformName parameter value set"
		missingParams = true
	}
	
	if(params.GITBranchTerraformName==null) {
		println "No GITBranchTerraformName parameter value set"
		missingParams = true
	}
	
	if(params.GITAccessTerraformCredentials==null) {
		println "No GITAccessTerraformCredentials parameter value set"
		missingParams = true
	}
	
    if(params.AWSAccesskeyTerraformID==null) {
		println "No AWSAccesskeyTerraformID parameter value set"
		missingParams = true
	}
	
	if(params.AWSSecretAccessTerraformKey==null) {
		println "No AWSSecretAccessTerraformKey parameter value set"
		missingParams = true
	}
	
	if(params.GITRepositoryGroovyName==null) {
		println "No GITRepositoryGroovyName parameter value set"
		missingParams = true
	}
	
    if(params.GITBranchGroovyName==null) {
		println "No GITBranchGroovyName parameter value set"
		missingParams = true
	}
	
	if(params.GITAccessGroovyCredentials==null) {
		println "No GITAccessGroovyCredentials parameter value set"
		missingParams = true
	}

    if(params.TerrafromAction==null) {
		println "No TerrafromAction parameter value set"
		missingParams = true
	}


	}


stage('Initialisation'){
	
	println "Checkout the GIT repo using below command"
	checkout scm
	
	dir('terraform') {
	git branch: params.GITBranchTerraformName, changelog: false, credentialId: params.GITAccessTerraformCredentials, poll: false, url: "${params.GITRepositoryTerraformName}"
	}
	
	//INFROMATIONS TO VERIFY 
	println "\n\n INFROMATION: \n\n" +
	        " Environment :                    ${params.Environment}\n" +
			" DataCenter :                     ${params.DataCenter}\n" +
			" GITRepositoryTerraformName:      ${params.GITRepositoryTerraformName}\n" +
			" GITBranchTerraformName:          ${params.GITBranchTerraformName}\n"
	        " GITAccessTerraformCredentials :  ${params.GITAccessTerraformCredentials}\n" +
			" AWSAccesskeyTerraformID :        ${params.AWSAccesskeyTerraformID}\n" +
			" AWSSecretAccessTerraformKey:     ${params.AWSSecretAccessTerraformKey}\n" +
			" GITRepositoryGroovyName:         ${params.GITRepositoryGroovyName}\n"
	        " GITBranchGroovyName :            ${params.GITBranchGroovyName}\n" +
	        " TerrafromAction :                ${params.TerrafromAction}\n" +			
			" GITAccessGroovyCredentials :     ${params.GITAccessGroovyCredentials}\n" 
		

	
	//DISPLAY THE BUILD DETAILS IN THE JENKINS CONSOLE 
	currentBuild.displayName ='aws-terraform-demo-ranga : DataCenter->' + params.DataCenter + ":" + params.Environment
	
 }
	
stage('User Confirmation') {
	if (params.Environment.trim().equals('')){
		input message: "Please confirm that you wish to execute the terraform in ${params.Environment} and Action is ${params.TerrafromAction} ?\n\n", ok: "Proceed"
	}else {
		input message: "Please confirm that you wish to execute the terraform in ${params.Environment} and Action is ${params.TerrafromAction} ?\n\n", ok: "Proceed"
	}
} 

stage('AWS Resource Provisioning - Terraform Execution') {
		
	sh script: "pwd;ls -lrt;cd terraform;ls -lrt; cd .."
	
	if(params.TerrafromAction=="apply") {
			println "TerrafromAction is apply"
			sh script: "/opt/terraform init ./terraform/demo-8"
			sh script: "sleep 30"
			sh script: "/opt/terraform plan /terraform/demo-8"
			sh script: "sleep 30"
			sh script: "/opt/terraform ${params.TerrafromAction} -auto-approve /terraform/demo-8"
		}else{
			sh script: "/opt/terraform ${params.TerrafromAction} -auto-approve  /terraform/demo-8"
		}
		//sh  script: 'rm -rf terraform'
	}

stage('AWS Terraform - CICD Pileline Execution End') {

	println "AWS - CICD Pileline Completed Successfully, Kindly check the Jenkins Console Log"
} 
}
