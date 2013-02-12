#!/usr/bin/env ruby


desc "Gets tonights local artist listings for your area."
task :get_local_listings do
  response_format = 'json'

  require 'net/http'
  remote_ip = Net::HTTP.get(URI 'http://remote-ip.herokuapp.com')

  current_date = Time.now.strftime('%F')
  search_date = current_date

  require 'httparty'
  artists = Array.new
  response = HTTParty.get("http://api.bandsintown.com/events/search.#{response_format}?location=#{remote_ip}&date=#{search_date}")
  response.each do |concert|
    concert['artists'].each do |artist|
      artists << artist['name']
    end
  end
  STDOUT.write "The artists playing in your area tonight are:\n"
  artists.each do |artist|
    STDOUT.write "-----> #{artist}\n"
  end
end

desc "Gets songs by artist from Rdio service."
task :get_artist_songs, :artist do |t, args|
  require 'rdio'
  artist = args.artist

  key = ENV['RDIO_KEY']
  secret = ENV['RDIO_SECRET']
  base = Rdio::BaseApi.new(key, secret)
  method = 'search'
  rdio_args = {
    "query" => artist,
    "types" => "artist",
    "count" => "1",
  }
  response = JSON.parse(base.call(method, rdio_args))
  top_artist_data = response['result']['results'].first
  p top_artist_data

  response = JSON.parse(base.call("get", {"keys" => top_artist_data['topSongsKey']}))
  response['result'][top_artist_data['topSongsKey']]['tracks'].each do |track|
    STDOUT.write "----> #{track['name']}\n"
  end
end
