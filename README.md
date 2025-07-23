# ungoogle-chromium-windows Portable Edition
![GitHub Actions Workflow Status](https://img.shields.io/github/actions/workflow/status/Silverwolf-x/ungoogled-chromium-plus/main.yml?event=schedule&label=UTC%2000%3A00%20schedule%20build)
![GitHub Tag](https://img.shields.io/github/v/tag/Silverwolf-x/ungoogled-chromium-plus?filter=meta-*&logo=yaml&label=CI%20version)
![GitHub Release](https://img.shields.io/github/v/release/Silverwolf-x/ungoogled-chromium-plus?include_prereleases&display_name=release&logo=googlechrome&label=ungoogled-chromium)
![GitHub Release](https://img.shields.io/github/v/release/Bush2021/chrome_plus?display_name=release&logo=github&label=Chrome%2B%2B)

Thanks to the contributions of the [ungoogled-software](https://github.com/ungoogled-software/ungoogled-chromium-windows) and [chrome\_plus](https://github.com/Bush2021/chrome_plus) projects.

The biggest advantage of ungoogled-chromium for me is its multifunctional search box that hides search history during use — a significant improvement over Chrome. However, ungoogled-chromium does not come in a portable format and automatically stores data in system folders like `C:\Users\[Name]\AppData\Local`.

By combining the `chrome_plus` project with the tutorial [How to Make Chrome Portable](https://www.bilibili.com/video/BV1gw4m1v7Sg/), this project attempts to integrate and automate the process using GitHub Actions.

* **Release** versions follow the update cycle of the `chrome_plus` project
* **Pre-releases** follow the update cycle of the `ungoogled-chromium-windows` project
* The workflow runs daily at 08:00 (UTC+8); actual execution may be delayed depending on GitHub Actions queue

