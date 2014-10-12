# -- WORK IN PROGRESS --

# Tutorial

ここでは、Voltで基本的なWebアプリケーションを作成する手順を示します。 このチュートリアルは、RubyとWeb開発の基本的な知識を持っていることを前提とします。

## Setup

First, lets install Volt and create an empty app.  Be sure you have ruby (>2.1.0) and rubygems installed.

Next install the volt gem:

    gem install volt

Using the volt gem, we can create a new project:

    volt new sample_project

This will setup a basic project in the sample_project folder.  We can ```cd``` into the folder and run the server:

    bundle exec volt server

Lastly, we can access the Volt console with:

    bundle exec volt console

