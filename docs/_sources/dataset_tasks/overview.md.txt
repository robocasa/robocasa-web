## Datasets
RoboCasa comes with a large selection of demonstrations to faciliate training agents. This includes human trajectories and machine-generated trajectories from [MimicGen]([https://www.anaconda.com/](https://mimicgen.github.io/)). At this time we are releasing human datasets and plan to release MimicGen datasets in the near future.

Here are a few ways to download the datasets:
```
python -m robocasa.scripts.download_datasets                                            # downloads all datasets
python -m robocasa.scripts.download_datasets --tasks PnPCounterToCab ArrangeVegetables  # downloads datasets for specific tasks
python -m robocasa.scripts.download_datasets --overwrite                                # overwrites existing datasets
python -m robocasa.scripts.download_datasets --ds_types human_raw                       # lite download: download human datasets without images
```

By default, all datasets are stored under `datasets/` in the root robocasa directory.