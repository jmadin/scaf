# Project Scaffolding in R

This is a work in progress. There is only one R function in this package that can be old here:

[R/scaf.R](R/scaf.R)

Here it is i you just want to copy it:

	scaf <- function(project_name) {

		project_name

		project <- try(system(paste("mkdir", project_name), ignore.stderr=TRUE))

		if (project == 1) {
			cat(paste("Warning: a directory called", project_name, "already exists. Choose a different project name.\n"))
		} else {

			setwd(project_name)

			system("mkdir doc")
			system(paste0("touch doc/", project_name, ".md"))
			system("mkdir data")
			system("mkdir R")
			system("mkdir output")
			system("mkdir output/figs")
			system("touch analysis.R")
			system("touch R/functions.R")
			system("touch README.md")
			system(paste("echo '#", project_name, "' > README.md"))

			cat("Project directories and files successfully created.\n")

			git <- try(system("git init", ignore.stdout=TRUE))
			if (git == 1) {
				cat("Warning: Git could not be initiatlised. Is it installed? You can initialise Git yourself later using 'git init' in the project directory.\n")
			} else {
				system("touch .gitignore")
				cat("Git succesfully initiatlised and '.gitignore' file added.\n")
			}

			cat(paste("Project", project_name, "successfully created.\n"))
		}
	}
