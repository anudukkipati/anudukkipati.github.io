---
layout: post
title:      "CLI Data Gem Project"
date:       2020-01-11 15:38:07 -0500
permalink:  cli_data_gem_project
---


I finally reached my first portfolio project, namely, CLI Data Gem Portfolio Project. It requires us to build a Ruby gem that provides a Command Line Interface to an external data source. It involves object-oriented programming to scrape data from a website and present it to a user via the terminal.  I decided to provide a list of public libraries in Austin by scraping Austin Public Library’s website.

*Web scraping* is the act of parsing a web page’s HTML and getting the data needed from that HTML document. A *gem* is a software package that contains a Ruby application or library which can be used to extend functionality in applications. *Command Line Applications* are programs that interact entirely through the terminal.

Here are the steps I followed:
	First and foremost, I needed a file structure that I needed to start building this project and I could accomplish this by running `gem bundle <project name>`.  Since I am going to be scrapping Austin Public Library’s website for data , I named by project “austin_public_libraries.
	
	The file structure looks like:
   
					```
					               ├── bin
                             └── run (is an executable file)

                        ├── config
                           └── environment.rb (contains information about all files required to initialize the environment i.e., all the code required to run the application)
                        ├── lib (contains all the files that define what our program can do)
                            └── austin_public_libraries.rb
                       └── spec
                           ├── austin_public_libraries_spec.rb
                           └── spec_helper.rb
                      ├── austin_public_libraries.gemspec 
                      ├── Gemfile (contains information about files required to support the application – like gem dependencies)
					          
					```
					  
					

	 
	 
	 
	 Next I made sure I listed all the dependencies I needed in the gemspec file (bundler, pry, Nokogiri) and ran “bundle” to ensure that I had all the dependencies that I needed installed.

	Then I made sure the environment.rb had all the information needed and created a “run” file in the bin directory and added the information it needed to run the application.

	Since I wanted a user to be able to look at a list of libraries and choose a library from the list to see more details, I created three files in my lib folder, namely, scraper.rb (to create a Scraper class so that I can define a method to scrape the data from the HTML document), library.rb (to create a Library class so that I can use the information I get from Scraper class to create libraries and cli.rb (to create the CLI class which will deal with the logic of the program).

	I started off with creating the Scraper class to scrape data from the website with the help of “Nokogiri” and CSS selectors and then moved on to the Library class where  I defined methods to create libraries and then save them to a class variable. Finally, I worked on CLI class to create logic so that a user is displayed options to choose from to view the data.

	Since there are no test files to test my code, I used “pry” to troubleshoot the code as needed.

I was a bit nervous as I started on this exciting project, but I did manage to get it to work. After finishing this project, I felt as if all the material that I learned is kind of coming together. 
	 
	 





	

