# udacity-pwa

    var cacheName = 'dogs-v1'
      var cacheFiles = [
          './',
          './bundle.js'
      ]

      self.addEventListener('install', function (e) {
          console.log('install', e)
          e.waitUntil(
              caches.open(cacheName).then(function (cache) {
                  console.log('caching...')
                  return cache.addAll(cacheFiles)
              })
          )
      })

      self.addEventListener('activate', function (e) {
          console.log('activate', e)
      })

      self.addEventListener('fetch', function(event) {
          event.respondWith(
            caches.match(event.request)
              .then(function(response) {
                // Cache hit - return response
                if (response) {
                  return response;
                }

                var requestClone = event.request.clone()

                return fetch(requestClone).then(function (res) {
                    if (!res || res.status !== 200 || res.type !== 'basic') {
                        return res
                    }

                    var responseClone = res.clone()
                    caches.open(cacheName).then(function (cache) {
                      cache.put(event.request, responseClone)
                    })

                  return response
                })


              }
            )
          )
      })
      
      
      <meta name="theme-color" content="#FCD500">
      <link rel="manifest" href="manifest.json">
      
      
      if ('serviceWorker' in navigator) {
        window.addEventListener('load', function () {
          navigator.serviceWorker.register('service-worker.js', { scope: '/' }).then(function (registration) {
            console.log('ServiceWorker registration successful with scope: ', registration.scope)
          }).catch(function (err) {
            console.log(err)
          })
        })
      }
      
    const Mock = [
        {img: 'https://pbs.twimg.com/media/Bz6t7HlIgAEax8E.jpg:large', title: 'Dog1'},
        {img: 'https://i.imgur.com/FjHheAA.jpg', title: 'Dog2'},
        {img: 'https://i.ytimg.com/vi/Doxj7ACZSe4/hqdefault.jpg', title: 'Dog3'},
        {img: 'https://www.biography.com/.image/t_share/MTQ3NjM5ODIyNjU0MTIxMDM0/snoop_dogg_photo_by_estevan_oriol_archive_photos_getty_455616412.jpg', title: 'Snoop Dogg'}
      ]
