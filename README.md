# EDA-Course-Proj_01
plots with R code for the first peer-graded assignment in the Exploratory Data Analysis course

pwr.dat <- subset(household_power_consumption, subset = Date == "1/2/2007" | Date == "2/2/2007")
str(pwr.dat)
rm(household_power_consumption)

#### ---- PLot 1 ---- ####
hist(pwr.dat$Global_active_power, col = "red", main = "Global Active Power", xlab = "Global Active Power (kilowatts)")
dev.copy(device = png, file = "plot1.png", width = 480, height = 480)
dev.off()

#### ---- Combining Date and Time ---- ####
pwr.dat$Date <- as.Date(pwr.dat$Date, format = "%d/%m/%Y")
pwr.dat <- transform(pwr.dat, dat.tim = as.POSIXct(paste(Date, Time)), "%d/%m%Y %H:%M:%S")
pwr.dat <- pwr.dat[-11]

#### ---- Plot 2 ---- ####
plot(x = pwr.dat$dat.tim, y = pwr.dat$Global_active_power, type = "l", xlab = "", ylab = "Global Active Power (kilowatts)")
dev.copy(png, file = "plot2.png", width = 480, height = 480)
dev.off()

#### ---- PLot 3 ---- ####
plot(x = pwr.dat$dat.tim, y = pwr.dat$Sub_metering_1, type = "l", xlab = "", ylab = "Energy sub metering")
lines(x = pwr.dat$dat.tim, y = pwr.dat$Sub_metering_2, col = "red")
lines(x = pwr.dat$dat.tim, y = pwr.dat$Sub_metering_3, col = "blue")
legend("topright", col = c("black", "red", "blue"), legend = c("Sub_metering_1", "Sub_metering_2", "Sub_metering_3"), lty = c(1,1,1),
       lwd = c(1,1,1))
dev.copy(png, file = "plot3.png", width = 480, height = 480)
dev.off()

#### ---- Plot 4 ---- ####
par(mfrow = c(2,2))
plot(x = pwr.dat$dat.tim, y = pwr.dat$Global_active_power, type = "l", xlab = "", ylab = "Global Active Power")
plot(x = pwr.dat$dat.tim, y = pwr.dat$Voltage, type = "l", xlab = "datetime", ylab = "Voltage")
plot(x = pwr.dat$dat.tim, y = pwr.dat$Sub_metering_1, type = "l", xlab = "", ylab = "Energy sub metering")
lines(x = pwr.dat$dat.tim, y = pwr.dat$Sub_metering_2, col = "red")
lines(x = pwr.dat$dat.tim, y = pwr.dat$Sub_metering_3, col = "blue")
legend("topright", col = c("black", "red", "blue"), legend = c("Sub_metering_1", "Sub_metering_2", "Sub_metering_3"), lty = c(1,1,1),
       lwd = c(1,1,1), bty = "n", cex = 0.5)
plot(x = pwr.dat$dat.tim, y = pwr.dat$Global_reactive_power, type = "l", xlab = "datetime", ylab = "Global_reactive_power")
dev.copy(png, file = "plot4.png", width = 480, height = 480)
dev.off()
