          :::::::::   ::::::::  :::        :::        :::::::: ::::::::::: :::::::::: :::::::::    |                   ,*
         :+:    :+: :+:    :+: :+:        :+:       :+:    :+:    :+:     :+:        :+:    :+:    |                 ,*
        +:+    +:+ +:+    +:+ +:+        +:+       +:+           +:+     +:+        +:+    +:+     |             ,*,*
       +#++:++#+  +#+    +:+ +#+        +#+       +#++:++#++    +#+     +#++:++#   +#++:++#:       |     ,*,   ,*
      +#+        +#+    +#+ +#+        +#+              +#+    +#+     +#+        +#+    +#+       |   ,*   *,*
     #+#        #+#    #+# #+#        #+#       #+#    #+#    #+#     #+#        #+#    #+#        | ,*
    ###         ########  ########## ########## ########     ###     ########## ###    ###         |*
                                                                                                    - - - - - - - - - - - 
  

A Ruby wrapper for the [HuffPost Pollster API](http://elections.huffingtonpost.com/pollster/api) 
which provides access to political opinion poll data and trend estimates from The Huffington Post.

The Pollster gem has been tested under Ruby 1.8.7, 1.9.2 and 1.9.3.

## Installation

  gem install pollster

## Usage Examples

    require 'pollster'
    include Pollster

See the current estimate of the president's job approval

    Pollster::Chart.find('obama-job-approval').estimates

List all charts about 2012 senate races

    Pollster::Chart.where(:topic => '2012-senate')

List all charts about Wisconsin

    Pollster::Chart.where(:state => 'WI')

Calculate the margin between Obama and Romney from a recent general election poll

    chart = Pollster::Chart.find('2012-general-election-romney-vs-obama')
    poll = chart.polls.first
    question = poll.questions.detect { |question| question[:chart] == chart.slug }
    obama = question[:responses].detect { |response| response[:choice] == "Obama" }
    romney = question[:responses].detect { |response| response[:choice] == "Romney" }
    margin = obama[:value] - romney[:value]

See the methodology used in recent polls about the Affordable Care Act

    chart = Chart.find 'us-health-bill'
    chart.polls.map { |poll| [poll.pollster, poll.method] }

## Authors

Aaron Bycoffe, bycoffe@huffingtonpost.com
Jay Boice, jayb@huffingtonpost.com

## Copyright

Copyright © 2012 The Huffington Post. See LICENSE for details.