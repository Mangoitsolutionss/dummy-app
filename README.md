  @@public_path = File.join(File.expand_path("../../", __FILE__), 'public', 'pages')

  def call(env)
    if  env["PATH_INFO"] == "/"
      [200, {"Content-Type" => "text/html"}, [get_body('homepage')]]
    else
      [200, {"Content-Type" => "text/html"}, [get_body(env['PATH_INFO'])]]
    end
  end

  private

  def get_body(filename)
    begin
      file = File.open(file_path(filename))
      body = file.read
      file.close
      body
    rescue
      "page not found"
    end
  end

  def file_path(filename)
    filename << '.html' unless filename =~ /\.html$/
    File.join(@@public_path, filename)
  end
end
