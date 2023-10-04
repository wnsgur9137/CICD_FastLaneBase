desc "build app and upload to testflight"
lane :testflight do
  get_certificates
  get_provisioning_profile
  increment_build_number(
	build_number: latest_testflight_build_number + 1
  )
  build_app(
	configuration: "Debug"
  )
  upload_to_testflight
  
  /*
  slack(
    message: "Testflight 배포되었습니다.",
	slack_url: "https://hooks.slack.com/{slack link}"
  )
  */

  /* error exception
  error do |lane, exception, options|
    slack(
	  message: "ERROR: #{exception}",
	  success: false,
	  slack_url: "https://hooks.slack.com/{slack link}"
	)
  end
  */
end

desc "build app and release to App Store."
lane :release do |options|
  if options[:v]
	get_certificates
	get_provisioning_profile
	increment_build_number(
	  build_number: latest_testflight_build_number + 1
	)
    build_app(
	  configuration: "Release"
	)
	upload_to_app_store(
	  app_version: options[:v],
	  submit_for_review: true,
	  force: true,
	  automatic_release: true,
	  skip_screenshots: true,
	  skip_metadata: false,
	)
	/* slack */
	/*
	slack(
	  message: "AppStore 심사 요청되었습니다.",
	  slack_url: "https://hooks.slack.com/{slack link}"
	)
	*/
  end
end
