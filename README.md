# Logstash Plugin

This is a plugin for [Logstash](https://github.com/elastic/logstash).

It is fully free and fully open source. The license is Apache 2.0.

## Documentation

Gets aidmaster and data files from CrowdStrike Falcon Data Replicator.  Returns each JSON document as log to be used in normal Logstash filter operations.

This plugin is based on the logstash-input-s3-sns-sqs plugin ( https://github.com/cherweg/logstash-input-s3-sns-sqs ).   Minor modifications have been made to match the FDR schema.


## Installation

logstash-plugin install logstash-input-crowdstrike_fdr

## Example

input { 

	# logstash-plugin install logstash-input-crowdstrike_fdr
	crowdstrike_fdr {
		# Must use new URL format:     https://github.com/aws/aws-sdk-ruby/issues/1620
		queue 						=> "https://sqs.us-west-1.amazonaws.com/<YOUR FDR DETAILS HERE>"
		region                     => "us-west-1"    # though this seems redundant,  we still need it for the S3 operations
		access_key_id            	=> "<YOUR KEY ID>"
		secret_access_key      		=> "<YOUR SECRET>"
		temporary_directory 		=> "logstash-s3-scratch"  # for storage of downloaded gzip files while processing
		sqs_delete_on_failure      => false
		sqs_skip_delete            => true     # don't delete files while testing
		visibility_timeout         => 120  # seconds     # adjust as needed
	}
}



## Need Help?

Need help? Try #logstash on freenode IRC or the https://discuss.elastic.co/c/logstash discussion forum.

