# Build

```
 docker build -t g4bzh/sopare -f Dockerfile .
```

# Run

```
docker run --device /dev/snd -v $PWD/asoundrc:/root/.asoundrc  -it g4bzh/sopare /bin/bash   
```


# Using Sopare

## Train a word or sentence

```
python sopare.py -t "test"
```

Do it at least 3 times
Register training

```
python2 sopare.py -c
```


## Run

Run (infinite loop with verbose)

```
./sopare.py -v -l
```

Run once

```
./sopare.py -v -l
```

Run once outputting last match

```
./sopare.py 2>/dev/null | tail -n 1 | rev | cut -d "'" -f 2 | rev
```

## Remove

## Remove train word or sentence

```
python sopare.py -d "test"
```

or all trainings

```
python sopare.py -d "*"
```

## Remove raw data

```
rm dict/*.raw
```
