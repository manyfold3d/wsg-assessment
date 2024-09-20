require 'json'
require 'net/http'
require 'date'

namespace :generate do
  task :markdown do
    json = JSON.parse(Net::HTTP.get(URI.parse("https://w3c.github.io/sustyweb/guidelines.json")))
    File.open("out.md", "w") do |file|
      file.puts <<~EOD
        ---
        title: Sustainability Self-Assessment #{Date.today}
        layout: page
        ---
        Assessed against the #{json["title"]} version #{json["version"]} (#{json["edition"]}) on #{Date.today}.

        ## Contents
        {: .no_toc }

        <details markdown="block">
          <summary>
            Expand
          </summary>
        - TOC
        {:toc}
        </details>

        ## Methodology

        ## Conclusions

      EOD
      json["category"].each do |category|
        next unless ["2", "3", "4"].include?(category["id"])
        if category["guidelines"]
          file.puts <<~EOD
            ## Section #{category["id"]}. #{category["name"]}

          EOD
          category["guidelines"].each do |guideline|
            file.puts <<~EOD
              ### Guideline #{category["id"]}.#{guideline["id"]}. [#{guideline["guideline"]}](#{guideline["url"]})

              #{guideline["description"]}

              <details markdown="block">
              <summary>
              Criteria: #{guideline["criteria"].map{ |g| "⚪<!--🔴🟡🟢🟣-->" }.join(" ") }
              </summary>

              EOD
            guideline["criteria"].each do |criterion|
              file.puts <<~EOD
                #### #{criterion["title"]}

                #{criterion["description"]}

                {:.todo}
                Write assessment detail here.
                Change paragraph class to "bad", "ok", "good", or "na" to set the
                evaluation overall result, and set the relevant icon colour after
                the guideline summary.

              EOD
            end
            file.puts <<~EOD
              </details>

            EOD
          end
        end
      end
    end
  end
end
