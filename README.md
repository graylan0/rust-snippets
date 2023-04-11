# rust-snippets
counter app for rust
```
use iced::{
    button, executor, Application, Button, Column, Command, Container, Element, Settings, Text,
};
use iced::alignment::Alignment;

pub fn main() -> iced::Result {
    ChatBot::run(Settings::default())
}

struct ChatBot {
    increment_button: button::State,
    decrement_button: button::State,
    value: i32,
}

#[derive(Debug, Clone, Copy)]
pub enum Message {
    IncrementPressed,
    DecrementPressed,
}

impl Application for ChatBot {
    type Executor = executor::Default;
    type Message = Message;
    type Flags = ();

    fn new(_flags: ()) -> (ChatBot, Command<Message>) {
        (
            ChatBot {
                increment_button: button::State::new(),
                decrement_button: button::State::new(),
                value: 0,
            },
            Command::none(),
        )
    }

    fn title(&self) -> String {
        String::from("ChatBot")
    }

    fn update(&mut self, message: Message) -> Command<Message> {
        match message {
            Message::IncrementPressed => {
                self.value += 1;
            }
            Message::DecrementPressed => {
                self.value -= 1;
            }
        }

        Command::none()
    }

    fn view(&mut self) -> Element<Message> {
        let increment = Button::new(&mut self.increment_button, Text::new("+"))
            .on_press(Message::IncrementPressed);

        let decrement = Button::new(&mut self.decrement_button, Text::new("-"))
            .on_press(Message::DecrementPressed);

        let content = Column::new()
            .padding(20)
            .spacing(20)
            .align_items(Alignment::Center)
            .push(increment)
            .push(Text::new(self.value.to_string()).size(40))
            .push(decrement);

        Container::new(content)
            .width(iced::Length::Fill)
            .height(iced::Length::Fill)
            .center_x()
            .center_y()
            .into()
    }
}
```
